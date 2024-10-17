# Feature & Routing Documentation

## 1. Features

### 1.1 Filter Bikes

Trong màn hình **Screen2**, người dùng có thể lọc các loại xe đạp dựa trên loại xe (Roadbike, Mountain, All). Tính năng này được thực hiện qua việc sử dụng `useState` để lưu trạng thái loại xe được chọn và một bộ lọc đơn giản trên danh sách xe đạp.

#### Code mẫu:

```javascript
const [selectedType, setSelectedType] = useState("All");

const filteredBikes =
  selectedType === "All"
    ? bikes
    : bikes.filter((bike) => bike.type === selectedType);

{
  ["All", "Roadbike", "Mountain"].map((type) => (
    <TouchableOpacity
      key={type}
      style={[
        styles.filterButton,
        selectedType === type && styles.selectedFilter,
      ]}
      // Điểm nhấn chỗ này
      onPress={() => setSelectedType(type)}
    >
      <Text
        style={[
          styles.filterText,
          selectedType === type && styles.selectedFilterText,
        ]}
      >
        {type}
      </Text>
    </TouchableOpacity>
  ));
}
```

Người dùng có thể nhấn vào các nút lọc để thay đổi loại xe hiển thị.

### 1.2 OnPress Event

Ứng dụng sử dụng sự kiện **onPress** để điều hướng giữa các màn hình và tương tác với các thành phần UI như nút nhấn. Ví dụ, trong **Screen1**, người dùng có thể nhấn nút **Get Started** để điều hướng đến **Screen2**.

#### Code mẫu:

```javascript
<TouchableOpacity onPress={() => navigation.navigate("s2")}>
  <Text>Get Started</Text>
</TouchableOpacity>
```

### 1.3 Add to Cart và Yêu Thích

Tính năng thêm sản phẩm vào giỏ hàng và đánh dấu yêu thích được triển khai trong **Screen3**. Người dùng có thể nhấn vào nút "Add to cart" để thêm sản phẩm vào giỏ hàng, hoặc nhấn vào biểu tượng trái tim để đánh dấu yêu thích.

#### Code mẫu:

```javascript
const [isFavorite, setIsFavorite] = useState(false);

<TouchableOpacity onPress={() => setIsFavorite(!isFavorite)}>
  <Icon // Icon này là của paper
    source="heart"
    color={isFavorite ? "#FF6347" : "#000"}
    size={40}
  />
</TouchableOpacity>;
```

## 2. Routing (Điều hướng)

### 2.1 Cấu trúc điều hướng

Ứng dụng sử dụng thư viện `@react-navigation/native-stack` để quản lý điều hướng giữa các màn hình. Tất cả các màn hình được khai báo trong `App.tsx` và được điều hướng thông qua đối tượng `navigation`.

#### Cấu trúc điều hướng:

```javascript
import { createNativeStackNavigator } from "@react-navigation/native-stack";
import { createStaticNavigation } from "@react-navigation/native";

const RootStack = createNativeStackNavigator({
  screens: {
    s1: Screen1,
    s2: Screen2,
    s3: Screen3,
  },
});

const Navigation = createStaticNavigation(RootStack);

export default function App() {
  return (
    <PaperProvider>
      <Navigation />
    </PaperProvider>
  );
}
```

### 2.2 Các màn hình

- **Screen1**: Màn hình giới thiệu cửa hàng, có nút điều hướng sang màn hình chính của danh sách xe đạp (**Screen2**).
- **Screen2**: Màn hình chính hiển thị danh sách xe đạp với các bộ lọc. Khi nhấn vào một sản phẩm, ứng dụng sẽ điều hướng đến màn hình chi tiết sản phẩm (**Screen3**).
- **Screen3**: Màn hình chi tiết sản phẩm, người dùng có thể xem thông tin chi tiết của sản phẩm, thêm sản phẩm vào giỏ hàng, và đánh dấu sản phẩm yêu thích.

### 2.3 Code điều hướng mẫu từ **Screen2** đến **Screen3** có truyền tham số:

```javascript
import { useNavigation } from "@react-navigation/native";

const navigation = useNavigation();

<TouchableOpacity
  onPress={() => {
    navigation.navigate("s3", { bike: item });
  }}
>
  <Text>{item.name}</Text>
</TouchableOpacity>;
```

### 2.4 Nhận tham số từ navigate

Ứng dụng truyền dữ liệu xe đạp từ **Screen2** sang **Screen3** thông qua đối tượng `route.params`. Điều này cho phép hiển thị chi tiết của sản phẩm được chọn.

#### Code mẫu:

```javascript
export default function Screen3({ route }) {
  ...
  const { bike } = route.params;
  <Image source={bike.image} />
  <Text>{bike.name}</Text>
  ...
}
```
