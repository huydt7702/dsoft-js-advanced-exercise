# Mục lục

1. [Ưu nhược điểm của các phương thức làm việc với mảng](#advantages-disadvantages)
2. [Test performance trên các phương thức làm việc với mảng phổ biến](#test-performance)
3. [So sánh phương thức `.splice()` vs `.slice()`](#splice-slice-difference)
4. [So sánh `spread operator` vs `.concat()`](#spread-concat-difference)
5. [So sánh `new Array()` vs `[]`](#newArray-brackets-difference)
6. [So sánh `new Array()` vs `Array()`](#newArray-Array-difference)
7. [So sánh `.at(index)` vs `array[index]`](#at-array[index]-difference)
8. [So sánh `.findIndex()` vs `.indexOf()`](#findIndex-indexOf-difference)

## Ưu nhược điểm của các phương thức làm việc với mảng <a name="advantages-disadvantages"></a>

`JavaScript` là ngôn ngữ lập trình mạnh mẽ và linh hoạt, đặc biệt là khi làm việc với mảng dữ liệu. Trong phần này, chúng ta sẽ đi vào so sánh ưu nhược điểm của các hàm thao tác mảng phổ biến nhất trong `JavaScript`.

1. `forEach()`

- **Ưu điểm**:
  - Dễ sử dụng, cú pháp rõ ràng, phù hợp để lặp qua các phần tử trong mảng và thực hiện hành động trên mỗi phần tử.
- **Nhược điểm**:
  - Không thể break khỏi vòng lặp (như các vòng lặp `for` hoặc `while`)
  - Không trả về một giá trị mới từ vòng lặp.

2. `map()`

- **Ưu điểm**:
  - Trả về một mảng mới được biến đổi từ mảng ban đầu.
  - Dễ dàng thay đổi giá trị mà không ảnh hưởng đến mảng gốc.
- **Nhược điểm**:
  - Không thể dừng hoặc bỏ qua các vòng lặp.

3. `filter()`

- **Ưu điểm**:
  - Trả về một mảng mới chỉ chứa các phần tử thỏa mãn điều kiện được chỉ định.
  - Dễ đọc và dễ sử dụng.
- **Nhược điểm**:
  - Không thể dừng hoặc bỏ qua các vòng lặp.

4. `reduce()`

- **Ưu điểm**:
  - Linh hoạt và mạnh mẽ, có thể thực hiện nhiều tác vụ khác nhau.
  - Trả về một giá trị duy nhất sau khi biến đổi mảng.
- **Nhược điểm**:
  - Cú pháp phức tạp hơn so với các phương thức khác.
  - Cần phải xác định giá trị khởi đầu cho biến kết quả.

5. `find()`

- **Ưu điểm**:
  - Trả về phần tử đầu tiên trong mảng thỏa mãn điều kiện được chỉ định.
  - Dễ đọc và dễ sử dụng.
- **Nhược điểm**:
  - Không thể sử dụng để biến đổi mảng.

6. `some()` và `every()`

- **Ưu điểm**:
  - Trả về một giá trị `boolean` dựa trên điều kiện được áp dụng cho tất cả hoặc một phần của mảng.
  - Giúp kiểm tra mảng một cách dễ dàng.
- **Nhược điểm**:
  - Chỉ trả về `true` hoặc `false`, không thể trả về các phần tử thỏa mãn điều kiện.
  - Không thể sử dụng để biến đổi mảng.

Mỗi hàm có những ưu nhược điểm riêng và được sử dụng trong các trường hợp cụ thể. Sự lựa chọn phụ thuộc vào yêu cầu cụ thể của bạn khi làm việc với mảng trong `JavaScript`.

## Test performance trên các phương thức làm việc với mảng phổ biến <a name="test-performance"></a>

Trong phần này chúng ta sẽ so sánh thời gian chạy của các cách được sử dụng phổ biến nhất để lặp qua một mảng trong JavaScript. <br> <br>
Để xem cách nào sẽ hiệu quả nhất nhé. <br> <br>
Let'go :))

- Ý tưởng rất đơn giản. Tớ đã so sánh thời gian chạy của năm cách rất phổ biến `(map, forEach, for, while, do while)` để lặp qua một mảng sử dụng một mảng có 100 giá trị và một mảng có 10 triệu giá trị. Code được chạy trong môi trường thực thi Node.js version `v20.11.0` trên một chiếc máy Laptop hệ điều hành `Linux ZorinOS 16.3`

#### Đầu tiên sẽ test performance của phương thức `.map()`

Đây là code được sử dụng cho 1 array gồm 100 giá trị

```js
const arraySize = 100;

const arrayToTest = Array(arraySize)
  .fill(0)
  .map((_, i) => i);

// small code to warm up the process used
for (let index = 0; index < arrayToTest; index++) {
  index * index + Math.sqrt(item);
}

console.time('map');
arrayToTest.map((item, index) => {
  return (arrayToTest[index] = item * item + Math.sqrt(item));
});
console.timeEnd('map');
```

Đây là kết quả tôi nhận được từ đoạn mã trên:

```js
map: 0.10888671875 ms
```

Rồi bây giờ đến array 10 triệu giá trị thử nhé, sử dụng lại code tương tự như trên và chỉ thay thế `arraySize` bằng `10000000`. <br> <br>
Và đây là kết quả mà chúng ta nhận được:

```js
map: 1090.72607421875 ms
```

#### Tiếp theo sẽ là phương thức `.forEach()`

Đây là code được sử dụng cho một mảng gồm 100 giá trị

```js
const arraySize = 100;

const arrayToTest = Array(arraySize)
  .fill(0)
  .map((_, i) => i);

// small code to warm up the process used
for (let index = 0; index < arrayToTest; index++) {
  index * index + Math.sqrt(item);
}

console.time('forEach');
arrayToTest.forEach((item, index) => {
  return (arrayToTest[index] = item * item + Math.sqrt(item));
});
console.timeEnd('forEach');
```

Đây là kết quả mà tớ nhận được từ đoạn code trên:

```js
forEach: 0.123046875 ms
```

Rồi bây giờ sẽ là array có `10000000` values, vẫn là sử dụng lại code ở trên chỉ thay thế `arraySize` bằng `10000000`. <br> <br>
Kết quả của chúng ta ở đây:

```js
forEach: 1164.68408203125 ms
```

#### Bây giờ sẽ test vòng for thường nhé

Đây là code được sử dụng cho một mảng gồm 100 giá trị

```js
const arraySize = 100;

const arrayToTest = Array(arraySize)
  .fill(0)
  .map((_, i) => i);

// small code to warm up the process used
for (let index = 0; index < arrayToTest; index++) {
  index * index + Math.sqrt(item);
}

console.time('for');
for (let i = 0; i < arrayToTest.length; i++) {
  arrayToTest[i] = arrayToTest[i] * arrayToTest[i] + Math.sqrt(arrayToTest[i]);
}
console.timeEnd('for');
```

Đây là kết quả mà tớ nhận được

```js
for: 0.10400390625 ms
```

Còn đối với mảng `10000000` value thì sao, thay thế lại arraySize bằng `10000000` nhé ae. <br> <br>
Bùmmm

```js
for: 150.463134765625 ms
```

#### Rồi bây giờ sẽ test vòng while

Vẫn bài toán cũ, đây là code được sử dụng cho một mảng gồm 100 giá trị

```js
const arraySize = 100;

const arrayToTest = Array(arraySize)
  .fill(0)
  .map((_, i) => i);

// small code to warm up the process used
for (let index = 0; index < arrayToTest; index++) {
  index * index + Math.sqrt(item);
}

console.time('while');
let i = 0;
while (i < arrayToTest.length) {
  arrayToTest[i] = arrayToTest[i] * arrayToTest[i] + Math.sqrt(arrayToTest[i]);
  i++;
}
console.timeEnd('while');
```

Và đây là kết quả mà tớ nhận được

```js
while: 0.115966796875 ms
```

Còn đối với array `10000000` values thì sao, vẫn như thường lệ, sử dụng lại code ở trên và cho `arraySize` bằng `10000000` <br> <br>

Kết quả của chúng ta ở đây:

```js
while: 150.797119140625 ms
```

#### Rồi giờ đến vòng do...while

Đây là code được sử dụng cho một mảng gồm 100 giá trị

```js
const arraySize = 100;

const arrayToTest = Array(arraySize)
  .fill(0)
  .map((_, i) => i);

// small code to warm up the process used
for (let index = 0; index < arrayToTest; index++) {
  index * index + Math.sqrt(item);
}

console.time('do while');
let i = 0;
do {
  arrayToTest[i] = arrayToTest[i] * arrayToTest[i] + Math.sqrt(arrayToTest[i]);
  i++;
} while (i < arrayToTest.length);
console.timeEnd('do while');
```

Và đây là kết quả của chúng ta:

```js
do while: 0.168212890625 ms
```

Rồi vẫn như thế nhé, thử với `arraySize` bằng `10000000` xem nào <br> <br>

Bùmmm

```js
do while: 175.574951171875 ms
```

#### Tóm tắt

Đối với mảng có 100 giá trị, đây là kết quả mà tớ nhận được

```js
map: 0.10888671875 ms
forEach: 0.123046875 ms
for: 0.10400390625 ms
while: 0.115966796875 ms
do while: 0.168212890625 ms
```

Còn đối với mảng có `10000000` giá trị thì

```js
map: 1090.72607421875 ms
forEach: 1164.68408203125 ms
for: 150.463134765625 ms
while: 150.797119140625 ms
do while: 175.574951171875 ms
```

- Trong trường hợp của mảng nhỏ, việc tối ưu hóa của trình biên dịch V8 khi biên dịch mã JavaScript của chúng ta là đủ tốt và thời gian chạy của các phương thức kiểm tra ở trên rất gần nhau.
- Tuy nhiên, đối với các mảng lớn, phương thức `.map()` và `.forEach()` mất nhiều thời gian hơn nhiều (hơn mười một lần như được thể hiện trong các ví dụ trên) so với các cách lặp mảng khác. Một yếu tố gây ra thời gian bổ sung này là việc gọi các hàm callback, điều này tiêu tốn nhiều bộ nhớ hơn và do đó thêm chi phí hiệu suất hơn đối với các mảng lớn. Các vòng lặp `for`, `while` hoặc `do while` có thời gian chạy rất gần nhau trên các mảng lớn và khó có thể nói, ít nhất từ các ví dụ trên thì `for`, `while` hay `do while` có thời gian chạy nhanh hơn đáng kể so với các method làm việc với mảng khác.

### Kết luận

Khi chúng ta phải viết một vòng lặp, việc xem xét xem giải pháp nào hoạt động tốt nhất là rất quan trọng. Trong các mảng tương đối nhỏ, công việc tối ưu hóa được thực hiện bởi trình biên dịch V8 là đủ tốt. Tuy nhiên, khi xử lý một lượng lớn dữ liệu, thì chi phí hiệu suất có thể quan trọng nếu chúng ta không chọn một giải pháp hiệu quả nhất một cách cẩn thận thì thời gian chạy khi đó có thể gấp 11 lần trong một số trường hợp như được thể hiện trong các kết quả ở trên.

## So sánh phương thức `.splice()` vs `.slice()` <a name="splice-slice-difference"></a>

- Khi làm việc với mảng trong JavaScript, có 2 phương thức thường được sử dụng để thao tác với mảng là `.slice()` và `.splice()`. Thoạt nhìn, chúng có vẻ giống nhau vì chúng phát ra âm thanh gần giống nhau và cả hai đều hoạt động với mảng, nhưng 2 phương thức này thực sự hoạt động hoàn toàn khác nhau.

- Trong phần này, chúng ta sẽ khám phá những điểm khác biệt chính giữa 2 phương thức `.slice()` và `.splice()` anh em nhé. Chúng ta sẽ xem xét cú pháp, tham số truyền vào, giá trị trả về và ví dụ về cách sử dụng của chúng để hiểu khi nào và tại sao lại sử dụng cái này so với cái kia. <br> <br>

Ok, Let's go

### Phương thức `.slice()`

Phương thức `.slice` tạo ra một bản sao (shallow copy) của một phần được chỉ định của mảng vào trong một mảng mới. Mảng ban đầu sẽ không bị thay đổi. <br> <br>

Một số điều quan trọng cần biết về `splice`.

#### Syntax và Parameters

```js
slice();
slice(begin);
slice(begin, end);
```

- **begin** - Optional. Vị trí bắt đầu. Mặc định là 0. Nếu là số âm thì chọn từ cuối mảng.
- **end** - Optional. Vị trí kết thúc. Mặc định là phần tử cuối cùng. Nếu là số âm thì chọn từ cuối mảng.

#### Giá trị trả về

Một mảng mới chứa các phần tử được chọn. Mảng ban đầu vẫn không thay đổi.

#### Một số ví dụ

Trích xuất một phần từ index 1 đến 3

```js
let fruits = ['Apple', 'Orange', 'Mango', 'Banana'];
let citrus = fruits.slice(1, 3); // Returns ['Orange', 'Mango']
```

Trích xuất từ ​​index 1 đến cuối mảng

```js
let fruits = ['Apple', 'Orange', 'Mango', 'Banana'];
let allCitrus = fruits.slice(1); // Returns ['Orange', 'Mango', 'Banana']
```

Trường hợp index là số âm

```js
let fruits = ['Apple', 'Orange', 'Mango', 'Banana'];
let lastTwo = fruits.slice(-2); // Returns ['Mango', 'Banana']
```

#### Tại sao nên sử dụng `.slice()`?

Sử dụng `.slice()` để trích xuất một phần của mảng thành một mảng mới mà không sửa đổi nó. Một số trường hợp sử dụng phổ biến:

- Tạo một mảng con hoặc bản sao của một phần của mảng hiện có
- Sao chép toàn bộ mảng để thực hiện các thao tác mà không thay đổi bản gốc
- Chia mảng thành nhiều mảng nhỏ hơn để xử lý
- Lấy ra một bản sao của mảng được truyền vào các hàm mà không làm thay đổi nó.

Phương thức `.slice()` tạo ra bản sao nông (shallow copy), không phải bản sao sâu (deep copy). Nó sao chép các tham chiếu đối tượng vào một mảng mới thay vì toàn bộ đối tượng.

### Phương thức `.splice()`

Phương thức `splice()` sửa đổi một mảng bằng cách xóa, thay thế hoặc chèn các mục vào một index đã chỉ định.

#### Syntax và Parameters

```js
array.splice(start, deleteCount, item1, item2, ...)
```

- **start** - Required. Index (vị trí) để thêm hoặc xóa các item. Nếu là giá trị âm thì được tính từ cuối mảng.
- **deleteCount** - Optional. Số lượng item cần loại bỏ.
- **item1, item2,...** - Optional. Các phần tử mới sẽ được thêm vào.

#### Giá trị trả về

Trả về một mảng chứa các phần tử đã bị xóa. Nếu chỉ thêm các phần tử, nó sẽ trả về một mảng trống.

#### Một số ví dụ

Xóa 1 phần tử tại index 1

```js
let fruits = ['Apple', 'Mango', 'Banana'];
let removed = fruits.splice(1, 1); // Returns ['Mango']
// fruits is ['Apple', 'Banana']
```

Nếu là số âm thì sao

```js
let fruits = ['Apple', 'Mango', 'Banana'];
let removed = fruits.splice(-1, 1); // Returns ['Banana']
// fruits is ['Apple', 'Mango']
```

Chèn các phần tử mà không xóa

```js
let fruits = ['Apple', 'Mango', 'Banana'];
fruits.splice(1, 0, 'Orange'); // Returns []
// fruits is ['Apple', 'Orange', 'Mango', 'Banana']
```

Xóa và chèn các phần tử

```js
let fruits = ['Apple', 'Mango', 'Banana'];
fruits.splice(1, 1, 'Lemon', 'Orange'); // Returns ['Mango']
// fruits is ['Apple','Lemon','Orange','Banana']
```

#### Tại sao nên sử dụng `.splice()`?

`.splice()` cho phép sửa đổi nội dung của một mảng bằng cách xóa hoặc chèn các phần tử mà không cần phải tạo ra một mảng mới. <br> <br>

Một số trường hợp sử dụng phổ biến của `splice()`

- Chèn phần tử vào bất kỳ chỉ mục (index) nào
- Xóa các phần tử theo chỉ mục hoặc giá trị
- Thay thế các phần tử bằng cách kết hợp việc xóa và chèn.
- Xóa sạch các phần tử của mảng
- Sắp xếp lại các phần tử của mảng bằng cách di chuyển chúng

### Sự khác biệt chính giữa `.slice()` và `.splice()` trong JavaScript

Mặc dù `.slice()` và `.splice()` có vẻ giống nhau nhưng chúng hoạt động hoàn toàn khác nhau

- **Modification** - `.slice()` trích xuất các phần tử thành một mảng mới mà không sửa đổi mảng gốc. `.splice()` thay đổi nội dung của mảng ban đầu.
- **Parameters** - `.slice()` có hai tham số optional, index bắt đầu và kết thúc. `.splice()` bắt buộc index bắt đầu và optional deleteCount.
- **Return value** - `.slice()` trả về các phần tử được cắt trong một mảng mới. `.splice()` trả về các phần tử đã bị xóa trong một mảng.
- **Use cases** - `.slice()` để đọc mảng mà không gây thay đổi. `.splice()` để thực hiện các thay đổi bằng cách chèn/xóa phần tử.

### Kết luận

Phương thức `.slice()` tạo ra một mảng mới bằng cách sao chép các phần tử từ một mảng hiện có mà không làm thay đổi mảng cũ. Điều này hữu ích để sao chép hoặc loại bỏ một phần của các phần tử mảng. Phương thức `.splice()` trực tiếp thay đổi mảng gốc bằng cách chèn, xóa hoặc thay thế các phần tử tại chỉ mục được chỉ định. Điều này hữu ích cho các thay đổi như sắp xếp lại các phần tử của mảng.

## So sánh `spread operator` vs `.concat()` <a name="spread-concat-difference"></a>

Sự khác biệt giữa `spread operator` và `.concat()`

Đây là đoạn code về `spread operator`

```js
let parts = ['four', 'five'];
let numbers = ['one', 'two', 'three'];
console.log([...numbers, ...parts]); // Return: ['one', 'two', 'three', 'four', 'five']
```

Và đây là đoạn code về `.concat()`

```js
let parts = ['four', 'five'];
let numbers = ['one', 'two', 'three'];
console.log(numbers.concat(parts)); // // Return: ['one', 'two', 'three', 'four', 'five']
```

Ồ!!! Cả hai đều cho ra kết quả giống nhau. Vậy, điểm khác biệt giữa chúng là gì? Và cái nào performance tốt hơn? Hãy cùng tớ tìm hiểu nhé :)) <br> <br>

Let's go <br> <br>

`.concat()` và `spread operator` rất khác nhau khi đối số không phải là một array. <br> <br>

- Khi đối số không phải là một array, `.concat()` thêm toàn bộ argument vào cuối mảng mà không thực hiện bất kỳ việc chia nhỏ hay lặp lại nào
- Trong khi `spread operator` cố gắng lặp qua mỗi phần tử của argument và thêm chúng vào mảng, do đó kết quả sẽ bị chia nhỏ thành các phần tử riêng biệt. <br> <br>

Đây là ví dụ:

```js
const a = [1, 2, 3];
const x = 'hello';

console.log(a.concat(x)); // [ 1, 2, 3, 'hello' ]
console.log([...a, ...x]); // [ 1, 2, 3, 'h', 'e', 'l', 'l', 'o' ]
```

Ở đây, `.concat()` xem chuỗi 'hello' là một phần tử duy nhất, trong khi `spread operator` cố gắng lặp qua từng ký tự của chuỗi.

Một ví dụ khác:

```js
const x = 99;

console.log(a.concat(x)); // [1, 2, 3, 99]
console.log([...a, ...x]); // TypeError: x is not iterable
```

`.concat()` coi số 99 là một phần tử duy nhất, trong khi `spread operator` cố gắng lặp qua nó và fail vì number không thể lặp qua. <br> <br>

Kết luận lại, khi argument có thể không phải là một mảng, lựa chọn giữa `.concat()` và `spread operator` phụ thuộc vào việc bạn muốn chúng được lặp qua hay không. <br> <br>

Ngoài ra, `ES6` cung cấp một cách để ghi đè hành vi mặc định của `.concat()` bằng `Symbol.isConcatSpreadable`. Mặc định, symbol này là `true` cho mảng và `false` cho mọi thứ khác. Đặt nó thành `true` sẽ khiến `.concat()` thử lặp qua argument, giống như `spread operator`. <br> <br>

```js
const str1 = 'hello';
console.log([1, 2, 3].concat(str1)); // [1,2,3, 'hello']

const str2 = new String('hello');
str2[Symbol.isConcatSpreadable] = true;
console.log([1, 2, 3].concat(str2)); // [ 1, 2, 3, 'h', 'e', 'l', 'l', 'o' ]
```

Hiệu suất của `.concat()` nhanh hơn, có lẽ vì nó có thể được tối ưu hóa cho mảng, trong khi `spread operator` phải tuân theo giao thức lặp chung. <br> <br>

Hãy cùng tớ test timings nào:

```js
let big = new Array(1e5).fill(99);
let i, x;

console.time('concat-big');
for (i = 0; i < 1e2; i++) x = [].concat(big);
console.timeEnd('concat-big');

console.time('spread-big');
for (i = 0; i < 1e2; i++) x = [...big];
console.timeEnd('spread-big');

let a = new Array(1e3).fill(99);
let b = new Array(1e3).fill(99);
let c = new Array(1e3).fill(99);
let d = new Array(1e3).fill(99);

console.time('concat-many');
for (i = 0; i < 1e2; i++) x = [1, 2, 3].concat(a, b, c, d);
console.timeEnd('concat-many');

console.time('spread-many');
for (i = 0; i < 1e2; i++) x = [1, 2, 3, ...a, ...b, ...c, ...d];
console.timeEnd('spread-many');
```

Kết quả ở đây:

```js
concat-big: 45.1279296875 ms
spread-big: 451.43701171875 ms

concat-many: 0.338134765625 ms
spread-many: 15.35009765625 ms
```

## So sánh `new Array()` vs `[]` <a name="newArray-brackets-difference"></a>

Sự khác biệt thực sự giữa việc khai báo một mảng như thế này là gì?

```js
const myArray = new Array();
```

và

```js
const myArray = [];
```

Việc sử dụng `new Array()` có một tùy chọn bổ sung trong các tham số: nếu truyền một số vào `constructor`, sẽ nhận được một mảng có độ dài là số đó:

```js
x = new Array(5);
alert(x.length); // 5
```

Minh họa các cách khác nhau để tạo một mảng:

```js
const a = []; // these are the same
const b = new Array(); // a and b are arrays with length 0
const c = ['foo', 'bar']; // these are the same
const d = new Array('foo', 'bar'); // c and d are arrays with 2 strings

// these are different:
const e = [3]; // e.length == 1, e[0] == 3
const f = new Array(3); // f.length == 3, f[0] == undefined
```

- Một điểm khác biệt là khi sử dụng `new Array()`, bạn có thể thiết lập kích thước của mảng, điều này ảnh hưởng đến kích thước của `stack`. Điều này có thể hữu ích nếu bạn đang gặp phải tình trạng tràn `stack` (stack overflow), đó là điều xảy ra khi kích thước của mảng vượt quá kích thước của stack, và nó phải được tạo lại. Vì vậy, tùy thuộc vào trường hợp sử dụng, có thể có sự tăng `performance` khi sử dụng new Array() bởi vì bạn có thể ngăn chặn tình trạng tràn xảy ra.
- Còn một điểm khác biệt nữa là: `new Array(5)`thực sự không thêm 5 phần tử `undefined` vào mảng. Nó chỉ thêm không gian cho 5 phần tử. Hãy nhớ rằng việc sử dụng `Array` theo cách này sẽ gây khó khăn cho việc dựa vào `array.length` để tính toán.

Ví dụ minh họa:

```js
new Array(2).length; // 2
new Array(2)[0] === undefined; // true
new Array(2)[1] === undefined; // true
```

Chà!!!, có thể bạn nghĩ rằng `new Array(2)` tương đương với `[undefined, undefined]`, **nhưng KHÔNG!!!** <br> <br>

Hãy thử nó với vòng `.map()`

```js
[undefined, undefined].map((e) => 1); // [1, 1]
new Array(2).map((e) => 1); // "(2) [empty × 2]" in Chrome
```

Thấy không? Ngữ nghĩa là hoàn toàn khác nhau! Vậy tại sao lại như vậy?

Theo quy định `ES6 Spec 22.1.1.2`, nhiệm vụ của `new Array(len)` chỉ là tạo ra một mảng mới mà thuộc tính `length` của nó được thiết lập là đối số `len` và đó là tất cả, có nghĩa là không có **phần tử thực** nào trong mảng mới được tạo ra này.

Hàm `map()`, theo quy định `22.1.3.15`, trước tiên sẽ kiểm tra `HasProperty` sau đó gọi lại hàm `callback`

```js
new Array(2).hasOwnProperty(0); // false
[undefined, undefined].hasOwnProperty(0); // true
```

**Và đó là lý do tại sao bạn không thể mong đợi bất kỳ hàm lặp nào hoạt động như thông thường trên các mảng được tạo ra từ `new Array(len)`.**

## Vậy còn `new Array()` vs `Array()` khác gì nhau? <a name="newArray-Array-difference"></a>

Sự khác biệt giữa:

```js
const x = Array(); // Return: []
```

và

```js
const x = new Array(); // Return: []
```

Theo chuẩn, khi `Array` được gọi như một hàm thay vì như một `constructor`, nó tạo và khởi tạo một đối tượng Mảng mới. Do đó, cuộc gọi hàm `Array(…)` tương đương với biểu thức tạo đối tượng mới `new Array(…)` với các đối số tương tự.

Lý do có thể sử dụng `Array` mà không cần từ khóa `new` là vì bên trong nó thực hiện một trick phổ biến với các `contructor`

Như thế này:

```js
function Thing() {
  if (!(this instanceof Thing)) {
    return new Thing();
  }
  // ... define object
}
```

Nghĩa là, nếu bạn gọi `Thing()` nó sẽ gọi `new Thing()` cho bạn.

## So sánh `.at(index)` vs `array[index]` <a name="at-array[index]-difference"></a>

Điểm khác biệt giữa `.at(index)` và `array[index]`

```js
const arr = [1, 2, 3, 4, 5];
arr[2]; // Return: 3
```

```js
const arr = [1, 2, 3, 4, 5];
arr.at(2); // Return: 3
```

Chà!!, trông có vẻ như nó rất giống nhau nhề

**KHÔNG ĐÂU!!!**

Cùng mình tìm hiểu nhé điểm khác biệt ở đây là gì nhé:

Phương thức `Array.prototype.at()` đã được giới thiệu trên `MDN`. Nó có vẻ hữu ích hơn so với việc sử dụng dấu ngoặc vuông `arr[i]` vì có tùy chọn để chỉ định chỉ số bắt đầu từ cuối mảng, ví dụ: `arr.at(-1)` sẽ trả về phần tử cuối cùng của mảng arr.

```js
const arr = [1, 2, 3, 4, 5, 6];
arr.at(-1); // Return: 6
```

Tuy nhiên, có những hạn chế khi chuyển sang sử dụng nó:

- Đó là một phương pháp rất mới. Các trình duyệt cũ hơn sẽ không thể hiểu mã của bạn nếu bạn sử dụng nó, trừ khi bạn tạo một `polyfill`
- Mặt khác, vì đó là một phương thức mới, không ngạc nhiên nếu một số lượng đáng kể các nhà phát triển chưa biết về nó - việc sử dụng `.at()` có thể làm bối rối một số người (và khiến họ phải tìm kiếm). Điều này không có nghĩa là bạn không nên sử dụng nó, nhưng đây là một điều cần lưu ý.

À, còn một điểm khác biệt nữa là `Array.prototype.at()` chỉ để truy xuất phần tử trong mảng. Nó không thể được sử dụng để gán, nhưng `array[index]` thì có thể.

## So sánh `.findIndex()` vs `indexOf()` <a name="findIndex-indexOf-difference"></a>

Đoạn code sử dụng `.findIndex()`

```js
const numbers = [1, 2, 3, 4, 5];
numbers.findIndex((num) => num === 3); // Return: 2
numbers.findIndex((num) => num === 6); // Return: -1
```

Đoạn code sử dụng `.indexOf()`

```js
const numbers = [1, 2, 3, 4, 5];
numbers.indexOf(3); // Return: 2
numbers.indexOf(6); // Return: -1
```

Chà!!! có thể bạn nghĩ 2 hàm này có vẻ giống nhau, tại sao `JavaScipt` lại tạo ra 2 hàm hoạt động giống nhau như vậy nhỉ??

**LÀM GÌ CÓ CHUYỆN **`JAVASCRIPT`** LẠI TẠO RA 2 HÀM GIỐNG NHAU!!**

Vậy điểm khác biệt ở đây là gì? Hãy cùng tớ tìm hiểu nhé <3

Sự khác biệt chính là các tham số truyền vào của các hàm này:

- `.indexOf()` yêu cầu một giá trị làm tham số đầu tiên. Điều này làm cho nó là lựa chọn tốt khi bạn muốn tìm index của một giá trị trong các mảng chứa các loại dữ liệu nguyên thủy `(primitive types)`(như string, number hoặc boolean).
- `.findIndex()` yêu cầu một hàm `callback` làm tham số đầu tiên. Sử dụng hàm này nếu bạn cần tìm index trong các mảng chứa các loại dữ liệu không nguyên thủy `(non-primitive types)` (như objects) hoặc điều kiện tìm kiếm của bạn phức tạp hơn chỉ là một giá trị.

Một số vị dụ để hiểu hơn nào:

Trong ví dụ này tớ muốn tìm index trong một mảng chứa các object

```js
let fruits = [
  { type: 'Apple', quantity: 9 },
  { type: 'Banana', quantity: 2 },
  { type: 'Orange', quantity: 8 },
  { type: 'Pear', quantity: 777 },
];

let myIndex = fruits.findIndex((fruit) => fruit.type === 'Orange'); // Returns 2.
```

Rồi tiếp theo tớ sẽ tìm index của một array đơn giản hơn

```js
let fruits = ['Apple', 'Banana', 'Pear', 'Orange'];

let index = fruits.indexOf('Orange'); // Returns 3.
```
