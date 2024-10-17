# Lý thuyết về các thành phần UI trong React Native

## 1. View

`View` là một thành phần cơ bản trong React Native, dùng để chứa các thành phần UI khác. Nó hoạt động như một container, giúp định hình bố cục và hiển thị các thành phần con. Có thể tùy chỉnh `View` bằng cách thêm các thuộc tính như `flex`, `padding`, `margin` để bố trí các thành phần bên trong theo cách mà mình muốn.

### Ví dụ:

```javascript
import React from "react";
import { View, Text, StyleSheet } from "react-native";

export default function ExampleView() {
  return (
    <View style={{
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
    }}>
      <Text>Hello World</Text>
    </View>
  );
}

```

### Ví dụ sreen1 (bike):

```javascript
<View style={styles.container}>
  <Text style={styles.title}>
    A premium online store for sporter and their stylish choice
  </Text>
</View>
```

Trong ví dụ này, `View` được sử dụng để bao bọc `Text` và định dạng vị trí của các thành phần bằng thuộc tính `style`.

---

## 2. Text

`Text` được sử dụng để hiển thị văn bản trên màn hình. Có thể sử dụng `Text` để hiển thị văn bản thông thường hoặc kết hợp với các thành phần khác như `View` để tạo giao diện phức tạp hơn.

### Ví dụ:

```javascript
import React from "react";
import { Text } from "react-native";

export default function ExampleText() {
  return <Text>Hello React Native</Text>;
}
```

### Ví dụ từ screen3 (bike):

```javascript
<Text style={styles.bikeName}>{bike.name}</Text>
<Text style={styles.discountPrice}>15% OFF 1350$</Text>
```

Trong ví dụ này, `Text` được sử dụng để hiển thị tên và giá của một chiếc xe đạp, với mỗi đoạn văn bản được định dạng khác nhau dựa trên style.

---

## 3. FlatList

`FlatList` là một thành phần dùng để hiển thị danh sách các phần tử trong React Native. Nó rất tối ưu cho các danh sách lớn nhờ vào tính năng lazy loading, chỉ hiển thị những phần tử hiện tại và tải thêm khi cuộn xuống. Bạn có thể sử dụng `FlatList` để tạo danh sách cuộn theo chiều dọc hoặc chiều ngang.

Để tạo `FlatList` cần 3 thành phần: data, render item (cách từng item được hiển thị), flatlist.

### Ví dụ:

```javascript
import React from "react";
import { FlatList, Text, View } from "react-native";

const data = [
  { id: "1", name: "Item 1" },
  { id: "2", name: "Item 2" },
];

export default function ExampleFlatList() {
  return (
    <FlatList
      data={data}
      renderItem={({ item }) => (
        <View>
          <Text>{item.name}</Text>
        </View>
      )}
      keyExtractor={(item) => item.id}
    />
  );
}
```

Ở ví dụ này renderItem được viết lồng vào component `FlatList` luôn.

### Ví dụ từ screen2 (bike):

```javascript
const bikes: Bike[] = [
  {
    id: "1",
    name: "Pinarello",
    price: 1800,
    image: require("../assets/bike1.png"),
    description:
      "It is a very important form of writing as we write almost everything in paragraphs, be it an answer, essay, story, emails, etc.",
    type: "Mountain",
  },
  {
    id: "2",
    name: "Pina Mountai",
    price: 1700,
    image: require("../assets/bike2.png"),
    description:
      "It is a very important form of writing as we write almost everything in paragraphs, be it an answer, essay, story, emails, etc.",
    type: "Mountain",
  },
];

const renderBikeItem = ({ item }: { item: Bike }) => (
  <TouchableOpacity
    style={styles.bikeCard}
    onPress={() => {
      navigation.navigate("s3", { bike: item });
    }}
  >
    <TouchableOpacity style={styles.favoriteButton}>
      <Text style={styles.favoriteIcon}>♡</Text>
    </TouchableOpacity>
    <Image source={item.image} style={styles.bikeImage} />
    <Text style={styles.bikeName}>{item.name}</Text>
    <Text style={styles.bikePrice}>${item.price}</Text>
  </TouchableOpacity>
);

<FlatList
  data={filteredBikes}
  renderItem={renderBikeItem}
  keyExtractor={(item) => item.id}
  numColumns={2}
  columnWrapperStyle={styles.bikeList}
/>;
```

Trong ví dụ này, `FlatList` được sử dụng để hiển thị danh sách các chiếc xe đạp, mỗi chiếc xe được render bằng một thành phần riêng.

---
