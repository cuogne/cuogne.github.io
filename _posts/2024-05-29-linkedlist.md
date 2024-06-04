---
layout: post
description: >-
  Tìm hiểu về Singly Linked List - Danh sách liên kết đơn trong C++
title: Singly Linked List
date: 2024-05-29 01:00:00 +0700
categories: [Blog, Code]
---

Bài viết dựa trên sự tìm hiểu và học hỏi của mình, nếu có sai sót hãy inbox trực tiếp mình để mình fix nhé !

Mình cũng sẽ để link các nguồn mình đã tìm hiểu và học hỏi trong quá trình học lập trình cũng như trong quá trình mình viết bài này bên dưới cuối bài blog.

# Linked List - Danh sách liên kết
## Danh sách Liên kết là gì? 

Nó là một trong những cấu trúc dữ liệu cơ bản và quan trọng nhất trong lập trình và khoa học máy tính. Nó cho phép bạn lưu trữ và quản lý các phần tử dữ liệu theo một cách động, linh hoạt hơn so với mảng (array).

## Cấu tạo của Danh sách Liên kết (Linked List)

Trước hết thì bạn có thể hiểu đơn giản như cái tên của nó, thì nó là 1 dãy danh sách được kết nối với nhau thông qua các liên kết.

Còn chính xác nhất thì danh sách liên kết là một cấu trúc dữ liệu gồm một chuỗi các phần tử, mỗi phần tử được gọi là một node. Mỗi node chứa hai thành phần chính:

- Data : đây là phần dữ liệu của Node
- Next : con trỏ lưu trữ địa chỉ của Node kế tiếp trong danh sách (đó cũng là lý do nó thường được đặt tên là next)

Cú pháp khai báo của một Node trong C++

```console
struct Node {
    int data ;
    Node* next ;
};
```

![Cấu tạo của một Node](/img/linkedlist/node.png)
_Cấu tạo của một Node_

Kiểu dữ liệu của data có thể thay đổi tùy vào loại dữ liệu mà người dùng muốn quản lý.

## Các loại danh sách liên kết

Linked List có 3 loại chính:

- Danh sách liên kết đơn (Singly Linked List): Mỗi node chứa một con trỏ trỏ đến node kế tiếp.
- Danh sách liên kết đôi (Doubly Linked List): Mỗi node chứa hai con trỏ, một trỏ đến node kế tiếp và một trỏ đến node trước đó.
- Danh sách liên kết vòng (Circular Linked List): Node cuối cùng trỏ đến node đầu tiên, tạo thành một vòng khép kín. Có thể là liên kết đơn hoặc đôi.

Ở đây thì mình chỉ tập trung vào Danh sách liên kết đơn, vì đây là loại phổ biến nhất và dễ hiểu nhất trong các loại danh sách liên kết, được ứng dụng rộng rãi trong quá trình học tập cũng như làm việc.

# Singly Linked List - Danh sách Liên kết đơn
## Cấu tạo của DSLK đơn

Danh sách liên kết đơn cũng có cấu tạo gồm các Node được liên kết với nhau. 

Phần tử đầu tiên của một DSLK đơn sẽ được quản lý bởi một con trỏ Head, phần tử cuối cùng của một DSLK đơn sẽ được quản lý bởi con trỏ Tail.

Trên thực tế, lúc làm việc với DSLK đơn, bạn chỉ cần đúng 1 con trỏ Head ở đầu danh sách là đã có thể quản lý được DSLK đơn, bởi vì DSLK đơn chỉ có thể duyệt theo 1 chiều thôi.

Node cuối cùng của DSLK đơn sẽ luôn trỏ vào NULL(hoặc nullptr), báo hiệu sự kết thúc của DSLK đơn.

![Danh sách liên kết đơn](/img/linkedlist/eng_node.png)
_Cấu tạo của một DSLK đơn_

## Đặc điểm của DSLK đơn

Do danh sách liên kết đơn là một cấu trúc dữ liệu động, được tạo nên nhờ việc cấp phát động nên nó có một số ưu nhược điểm sau đây:

### 1. Ưu điểm
- Được cấp phát bộ nhớ khi chạy chương trình
- Có thể thay đổi kích thước một cách linh hoạt, không cần phải khai báo kích thước cố định như mảng. Kích thước tối đa phụ thuộc vào bộ nhớ khả dụng của RAM
- Chèn và xóa phần tử nhanh chóng. Độ phức tạp là O(1) nếu biết trước vị trí
- Các phần tử được lưu trữ ngẫu nhiên (không liên tiếp) trong RAM

### 2. Nhược điểm
- Duyệt chậm do phải duyệt qua từng Node trong danh sách. Độ phức tạp là O(n)
- Vì thế nên truy cập phần tử ngẫu nhiên rất chậm vì phải duyệt từ đầu danh sách đến phần tử cần tìm. (Tìm kiếm tuyến tính - Linear Search)
- Tốn bộ nhớ: Mỗi node cần phải cấp phát bộ nhớ để lưu con trỏ.
- Khó quản lý hơn: Việc quản lý các con trỏ phức tạp hơn, dễ gặp lỗi nếu bạn không nắm vững con trỏ.

## Các thao tác cơ bản trên DSLK đơn

### 1. Khai báo cú pháp của Node

```console
struct Node {
    int data ;
    Node* next ;

    // constructor
    Node(int x){
        data = x ;
        next = nullptr ;
    }
};
```
Ở đây mình sử dụng luôn Constructor để khởi tạo các data cụ thể, và để dễ quản lý thì mình chọn kiểu số nguyên (int)

Bạn nào không thích dùng constructor luôn như mình thì có thể viết 1 hàm riêng để cấp phát nhé, như bên dưới:

```console
Node *createNode (int data){
    Node* node = new Node ;
    node -> data = data ;
    node -> next = nullptr ;
    return node ;
}
```
Lúc dùng các bạn chỉ cần ghi:
```console
Node* newNode = createNode(100);
```
Là đã cấp phát thành công 1 node có data là 100 đó.

### 2. Thêm một phần tử vào Head hoặc Tail của linked list
``` console
void addData(Node*& head, int data){
    Node* newNode = new Node(data);
    if (head == nullptr){
        head = newNode ;
    }
    else {
        Node* temp = head ;
        while (temp -> next != nullptr){
            temp = temp -> next ;
        }
        temp -> next = newNode;
    }
}
```
Bên trên là một hàm thực hiện chức năng thêm data vào cuối linked list được quản lý bởi con trỏ head

Ở đây hàm addData nhận vào 2 tham số là con trỏ head và biến data. Tham số Node*& head là một tham chiếu đến một con trỏ. Điều này cho phép hàm sửa đổi con trỏ head trong hàm gọi.

#### a. Giải thích Code

```console
Node* newNode = new Node(data);
```
Ở đây, ta cấp phát động cho Node có tên là newNode với data được truyền vào từ hàm.

Cú pháp này chỉ khả dụng khi các bạn sử dụng constructor như mình. Nếu các bạn không dùng constructor như mình thì các bạn chỉ cần khai báo:

```console
Node* newNode = new Node {data,nullptr};
```

hoặc là nếu bạn nào viết hàm cấp phát như mình ở trên thì

```console
Node* newNode = createNode(data);
```

Tiếp theo là:

```console
if (head == nullptr){
    head = newNode ;
}
```
Ở đây, ta kiểm tra xem head có bằng nullptr hay không, tức là danh sách liên kết có đang rỗng không, không có phần tử. Nếu điều này đúng, ta lấy head gán bằng phần tử vừa được cấp phát ở trên. Vậy là danh sách liên kết đã có phần tử đầu tiên.

```console
else {
    Node* temp = head ;
    while (temp -> next != nullptr){
        temp = temp -> next ;
    }
    temp -> next = newNode;
}
```

Nếu danh sách đã có phần tử rồi, ta tạo một con trỏ temp tạm thời dể duyệt qua danh sách, tránh sử dụng trực tiếp con trỏ head.

Sau đó, tạo một vòng lặp để duyệt qua danh sách. Vòng lặp kết thúc chỉ khi vòng lặp duyệt tới phần tử cuối cùng trong linked list (lúc này node cuối đang trỏ vào nullptr đó)

Câu lệnh temp = temp -> next di chuyển đến nút tiếp theo trong danh sách

Khi thoát khỏi vòng lặp cũng là lúc con trỏ temp đã đi đến cuối danh sách, ta thực hiện thao tác lấy temp -> next = newNode. Vì lúc này khi thoát khỏi vòng lặp, temp -> next đang có giá trị là nullptr, nên chỉ cần gắn node mới cấp phát thì ngay lập tức node mới đã được thêm vào cuối danh sách

Hmm, đọc xong chắc hơi khó hiểu nên các bạn xem ví dụ minh họa với hình ảnh nhé

![Cấp phát động node mới](/img/linkedlist/cpdnewNode.png){: w="400" h="200" }
_Cấp phát động một Node mới có data là 10 và trỏ vào nullptr_

Ở trên là mình đang cấp phát cho 1 Node chứa data là 10, tương ứng với câu lệnh
```console
Node* newNode = new Node(10);
```
Bên dưới là Node mình vừa cấp phát và linked list hiện có của mình

![Node và LinkedList](/img/linkedlist/linkedlist.png)

Để thêm 1 Node vào trong linked list (ở đây mình xét 2 trường hợp cơ bản nhất là add vào đầu và đuôi của dslk nhé) thì ta làm như sau:

#### b. Đối với head

+ Bước 1: Lấy next của newNode trỏ vào head
+ Bước 2: Lấy head trỏ ngược lại vào node

![Trỏ vào head](/img/linkedlist/ptrtohead.png)

```console
newNode -> next = head ;
head = newNode ;

// 10 -> 40 -> 30 -> 60
```

#### c. Đối với tail

+ Bước 1: Tạo 1 Node tạm tên là temp để quản lí danh sách, tránh sử dụng trực tiếp head

![Bước 1](/img/linkedlist/buoc1.png)

```console
Node* temp = head ;
```

+ Bước 2: Duyệt cho temp đi đến node cuối cùng của danh sách

![Bước 2](/img/linkedlist/buoc2.png)

```console
while (temp -> next != nullptr){
    temp = temp -> next ;
}
// Khi thoát khỏi vòng lặp cũng là lúc temp ở node cuối cùng trong danh sách
```

>Ở đây chắc là có bạn thắc mắc tại sao điều kiện lại là temp -> next != nullptr mà không phải là temp != nullptr

> Khi temp != nullptr thì temp sẽ duyệt đến cuối cùng (kể cả nullptr), nên khi temp = nullptr thì vòng lặp sẽ ngừng, lúc đó thì kh có con trỏ next nào còn ở đó cả, vì temp lúc này đang ở nullptr rồi thì còn next ở đâu nữa =))))

> ![Nullptr](/img/linkedlist/nullptr.png){: w="400" h="200" }
> _Nếu temp = nullptr thì ra sao_

> Nên ta phải chặn trước bằng cách temp -> next != nullptr, tức là khi temp đang ở node cuối cùng thì con trỏ next của node đó sẽ trỏ vào nullptr, lúc đó thì ta sẽ biết được là node kế tiếp là nullptr nên sẽ dừng ở đây, không duyệt nữa.

+ Bước 3: Lấy con trỏ next của node cuối cùng trỏ vào node cần thêm vào trong danh sách (ở đây là newNode)

![Bước 3](/img/linkedlist/buoc3.png)

```console
temp -> next = newNode ;
// 40 -> 30 -> 60 -> 10
```

Vậy là chúng ta đã thêm thành công 1 node vào trong linked list rồi !!!

### 3. Thêm vào một vị trí đã biết trước trong Linked List

Ở trên chúng ta đã nói qua về cách thêm 1 node vào head và tail, vậy nếu giờ chúng ta thêm ở một vị trí không phải head và tail thì sao ?

Ở đây mình giả sử chúng ta biết trước giá trị của một node nào đó trong linked list nhé, mình gọi nó là x đi =))) (khi vào ví dụ mình sẽ cho một số cụ thể nào đó)

Mình sẽ sử dụng một kỹ thuật có tên gọi là "Hai con trỏ" để có thể thêm vào trước và sau của một phần tử dễ dàng hơn.

Còn hai con trỏ là gì hả =))) các bạn có thể search gg về kỹ thuật này nha, đại khái là ta sẽ sử dụng 2 biến để quản lý các phần tử ấy mà.

Thật ra vẫn có thể sử dụng 1 con trỏ, nhưng mà kỹ thuật 2 con trỏ được áp dụng khá nhiều nên mình muốn giới thiệu đến các bạn luôn. 

> Bên dưới mình vẫn sẽ giới thiệu cách sử dụng một con trỏ nhé

#### a. Thêm 1 node vào phía trước x

Bắt đầu từ thêm vào phía trước nhé =)))

```console
void addBeforeQ(Node*& head, int data, int x) {
    Node* node = new Node(data);

    if (head == nullptr || head -> data == x) {
        node -> next = head;
        head = node;
        return;
    }

    Node* cur = head;
    Node* prev = nullptr;

    while (cur != nullptr && cur->data != x) {
        prev = cur;
        cur = cur->next;
    }

    if (cur != nullptr) {
        node->next = cur;
        if (prev != nullptr) {
            prev->next = node;
        }
    }
}
```
Bên trên là đoạn code thực hiện việc thêm 1 node chứa data vào trước phần tử x

Mình sẽ giải thích từ từ nhé
```console
if (head == nullptr || head -> data == x) {
    node -> next = head;
    head = node;
    return;
}
```
Dòng này kiểm tra việc danh sách liên kết có đang rỗng hoặc là phần tử đầu tiên của danh sách liên kết đó trùng với phần tử x hay không.

Nếu điều này đúng, sẽ thực hiện gán node đó vào head

```console
Node* cur = head;
Node* prev = nullptr;
```
Đây chính là kỹ thuật mà mình nói lúc nãy, mình đã tạo ra 2 con trỏ cur(current) và prev(previous). Nó hoạt động ra sao, xem đoạn code bên dưới nhé.

```console
while (cur != nullptr && cur->data != x) {
    prev = cur;
    cur = cur->next;
}
```
Mỗi con trỏ trong mỗi bài toán đều sẽ có những vai trò riêng nhất định. Trong trường hợp này:
- Con trỏ cur sẽ làm nhiệm vụ lưu trữ node đứng trước
- Con trỏ prev sẽ làm nhiệm vụ lưu trữ node phía sau của cur

> Để dễ hiểu nhất, bạn cứ tưởng tượng cur là người đi trước, còn prev là người đi sau, và người đi sau đang đi lại những nước đi của người đi trước.

![Prev and Cur](/img/linkedlist/prevandcur1.png)
![Prev and Cur](/img/linkedlist/prevandcur2.png)
_Hình ảnh minh họa cách hoạt động của 2 con trỏ prev và cur_

Chúng ta sẽ sử dụng con trỏ cur để duyệt danh sách, con trỏ prev sẽ theo sau sau khi con trỏ cur qua node kế tiếp.

```console
prev = cur;
cur = cur->next;
```

Và cứ thế, khi cur -> data, tức là giá trị của node đó trùng với phần tử x, ta lập tức thoát vòng lặp

> Ở đây mình xét trường hợp các số khác nhau trong danh sách, không tính các phần tử x giống nhau. 
> Nếu danh sách có nhiều số bằng x thì với cách duyệt này ta sẽ tìm được phần tử x đầu tiên trong danh sách, với khác điều kiện khác như thêm vào phần tử x thứ 2, thứ 3,... trong danh sách thì mình không xét tới
{: .prompt-info }

```console
if (cur != nullptr) {
    node->next = cur;
    if (prev != nullptr) {
        prev->next = node;
    }
}
```

Đầu tiên, ta kiểm tra điều kiện trước xem cur có phải là nullptr không, vì trong trường hợp trên của vòng while, thì vòng lặp vẫn có thể thoát ra nếu cur = nullptr, tức là ta không tìm thấy phần tử x trong danh sách

Nếu thỏa điều kiện cur != nullptr thì ta tiến hành:
- Lấy con trỏ next của node cần thêm vào gán bằng cur
- Kiểm tra điều kiện của prev, nếu thỏa điều kiện, lấy next của prev trỏ vào node

Hmm, các bạn xem hình minh họa bên dưới nha

![Ảnh minh họa](/img/linkedlist/addbefore_1.png)

Ở đây, mình giả sử mình cần thêm 1 node có data là 10 vào trước phần tử 60 (thay x = 60 á)

Cách thức duyệt ở trên mình cũng đã nói rồi, nên mình sẽ không nói lại ở đây. Ở đây mình bàn về cách thêm phần tử 10 vào trước 60.
 
Cur đang nắm giữ node mang giá trị 60, còn prev đang nắm giữ node mang giá trị 30

![Lấy node -> next = cur](/img/linkedlist/addbefore_2.png)

```console
node -> next = cur;
```

Ta lấy next của node mà cur đang giữ trỏ vào node cần thêm vào, tạo luồng liên kết giữa 10 và 60

![Lấy prev -> next = node](/img/linkedlist/addbefore_3.png)

```console
prev -> next = node;
```

Lấy con trỏ next của node mà prev đang giữ, trỏ vào node cần thêm vào

![Hoàn thành](/img/linkedlist/addbefore_4.png)

Hình ảnh sau thi ta thêm node có giá trị là 10 vào trước node 60

Vậy là ta có 1 danh sách liên kết gồm 4 node là 40 -> 30 -> 10 -> 60

Đó là cách sử dụng 2 con trỏ để quản lý các node và cách tạo liên kết cho các node cần thêm vào

#### b. Thêm 1 node vào phía sau x
Nếu các bạn đã hiểu cách thêm 1 node vào trước x, thì thêm phía sau cũng tương tự v thoi không khác quá nhiều đâu =))))

```console
void addAfterX(Node*& head, int data, int x) {
    Node* node = new Node(data);

    if (head == nullptr) {
        head = node;
        return;
    }

    Node* prev = head;
    Node* cur = head->next;

    while (prev != nullptr && prev->data != x) {
        prev = cur;
        if (cur != nullptr) {
            cur = cur->next;
        }
    }

    if (prev != nullptr) {
        node->next = cur;
        prev->next = node;
    }
}
```

Ở đây có sự khác một xíu giữa 2 con trỏ. 
Bây giờ:
- Con trỏ prev sẽ nắm giữ phần head
- Con trỏ cur sẽ giữ node phía sau head (tức là head -> next) 

Và chúng ta sẽ dùng con trỏ prev để duyệt danh sách

> Điều kiện head có nullptr hay không đã check ở trên ròi nha

![Khởi tạo 2 con trỏ](/img/linkedlist/addafter_1.png)

```console
while (prev != nullptr && prev->data != x) {
    prev = cur;
    if (cur != nullptr) {
        cur = cur->next;
    }
}
```
Ở đây ta lấy prev = cur qua mỗi lần lặp và nhớ kiểm tra xem cur có bằng nullptr hay không, vì ta dùng prev để duyệt chính, còn cur đi trước nên ta không thể quản lý cur 1 cách trực tiếp được.

> Nếu cur = nullptr thì prev sẽ ở node cuối cùng, lúc này ta sẽ ngưng trỏ cur = cur -> next và chỉ còn kiểm tra prev thôi. Nếu prev = nullptr luôn thì cur = prev = nullptr, lúc này danh sách liên kết không tồn tại phần tử x.

Ở đây mình lấy ví dụ cho trường hợp cur = nullptr và prev đang ở node cuối luôn nha, các trường hợp khác cũng tương tự thoi với cách duyệt cũng tương tự như thêm vào trước vậy á.

![Buon ngu qua](/img/linkedlist/addafter_2.png)

Ở đây mình lấy ví dụ cần thêm node chứa data là 10 vào phía sau node chứa data là 60

Trên hình là cũng đã duyệt 2 con trỏ đi qua hết rùi nha

![Lấy node -> next = cur nè](/img/linkedlist/addafter_3.png)

```console
node -> next = cur ;
```

![Lấy prev -> next = node](/img/linkedlist/addafter_4.png)

```console
prev -> next = node ;
```

Cách thức cũng tương tự như thêm 1 node vào trước x vậy đó =))))

#### c. [Bonus] Sử dụng một con trỏ để duyệt thì sao =)))

Phần này mình dùng 1 con trỏ duy nhất để có thể thêm vào trước hoặc sau x. Cái này các bạn tự tìm hiểu nha (Mà đọc tới đây chắc hiểu hết mà, không khó lắm đâu, có thể tự suy luận ra được hehee)

Sau khi đọc xong cả 2 cách nếu thấy cách nào dễ hiểu hơn thì cứ sài cách đó nha =))) kết quả tương tự nhau nhma chỉ khác cách code thôi.

> Thật ra cũng có nhiều người thấy cách này dễ hơn, nhma mình muốn các bạn biết tới kỹ thuật 2 con trỏ á nên mới phân tích kỹ cách kia ở trên =)))

> that ra tai tao buon ngu qua nen t luoi viet do

- Thêm một node vào sau x

```console
void addAfterQ(Node*& head, int data, int x) {
    Node* node = new Node(data);
    Node* temp = head;

    while (temp != nullptr && temp->data != x) {
        temp = temp->next;
    }

    if (temp != nullptr) {
        node->next = temp->next;
        temp->next = node;
    }
}
```
- Thêm một node vào trước x

```console
void addBeforeQ(Node*& head, int data, int x) {
    Node* node = new Node(data);

    if (head == nullptr || head -> data == x) {
        node -> next = head;
        head = node;
        return;
    }

    Node* temp = head;

    while (temp->next != nullptr && temp->next->data != x) {
        temp = temp->next;
    }

    if (temp->next != nullptr) {
        node->next = temp->next;
        temp->next = node;
    }
}
```
### 4. Xóa một node trong linked list

Đã có thêm rồi thì tất nhiên phải có xóa chứ đúng không

Muốn xóa một node nào đó trong linked list, ta phải biết được nó là node nào, chứa data là gì, ở vị trí nào, thỏa điều kiện mà mình cần phải xóa không.

#### a. Xóa node là head

Dối với head thì chúng ta chỉ cần sử dụng 1 con trỏ duy nhất để duyệt thoi. Trong trường hợp này ta lấy chính con trỏ head luôn.

```console
void deleteHead(Node*& head){
    if (head == nullptr){
        return ;
    }

    Node* temp = head ;
    head = temp -> next ;
    delete temp ;
}
```

Đầu tiên, ta kiểm tra xem linked list có rỗng kh, nếu rỗng thì return luôn.

Ở đây, ta sẽ tạo 1 node tạm tên là temp để giữ node cần xóa (Trong trường hợp này chính là node được quản lí bởi head đó)

![](/img/linkedlist/deletehead1.png)

Sau đó, ta di chuyển head sang node kế tiếp bằng câu lệnh

```console
head = head -> next ;
```

![](/img/linkedlist/deletehead2.png)

Cuối cùng, chúng ta xóa node được giữ bởi temp bằng câu lệnh

```console
delete temp ;
```

![](/img/linkedlist/deletehead3.png)

Khi bạn xóa một node trong linked list, bạn thực sự đang giải phóng vùng nhớ mà node đó đang chiếm giữ. Điều này có nghĩa là dữ liệu được lưu trữ trong node đó và con trỏ đến node tiếp theo trong danh sách sẽ không còn tồn tại nữa.

Tuy nhiên, việc giải phóng vùng nhớ không tự động làm cho các con trỏ khác đang trỏ đến node đó trở thành NULL. Nếu bạn có một con trỏ khác đang trỏ đến node đã bị xóa, con trỏ đó sẽ trở thành "dangling pointer" (con trỏ bị treo), tức là nó đang trỏ đến một vùng nhớ không hợp lệ. Sử dụng dangling pointer có thể dẫn đến lỗi và làm cho chương trình của bạn không ổn định.

(Phần này mình sẽ đề cập ở bên dưới)

#### b. Xóa node là tail

Giờ chúng ta sẽ xóa node cuối cùng trong linked list, tức là node có con trỏ đang trỏ vào nullptr ấy

Mình sẽ dùng 2 con trỏ nhé (một con trỏ vẫn được nha)

```console
void deleteTail(Node*& head){
    if (head == nullptr){
        return ;
    }

    if (head -> next == nullptr){
        delete head ;
        head = nullptr ;
        return ;
    }

    Node* cur = head ;
    Node* prev = nullptr ;
    while (cur -> next != nullptr){
        prev = cur ;
        cur = cur -> next ;
    }

    delete cur ;
    if (prev != nullptr){
        prev -> next = nullptr ;
    }
}
```

2 vòng if đầu tiên chỉ là kiểm tra các điều kiện đặc biệt

- Nếu head == nullptr, tức là linked list rỗng thì return luôn thôi

- Nếu head -> next == nullptr, tức là linked list chỉ có 1 node duy nhất, lúc này node đó vừa là head, cũng vừa là tail nên ta thực hiện xóa node đó như xóa head vậy.

Sau khi đã kiểm tra, nếu kh có gì xảy ra, ta sẽ tạo 2 con trỏ cur và prev. Cách thức hoạt  của 2 con trỏ tương tự như 2 con trỏ trong phần [Thêm 1 node vào trước x](#a-thêm-1-node-vào-phía-trước-x) vậy nên mình sẽ không nói lại nhé.

![](/img/linkedlist/deletetail1.png)

Sau khi duyệt xong, 2 con trỏ của chúng ta sẽ ở vị trí như hình. Ta lập tức

```console
delete cur ;
```
xóa đi node cur, tức là node cuối cùng trong linked list.

![](/img/linkedlist/deletetail2.png)

Lúc này, con trỏ prev sẽ rơi vào trạng thái "danging pointer" như ở trên mình đã có nói qua. Vì vậy, để tiếp tục linked list. Ta sẽ

```console
if(prev != nullptr){
    prev -> next = nullptr ;
}
```

![](/img/linkedlist/deletetail3.png)

Vậy là ta đã thành công xóa đi node cuối cùng trong linked list rồi

#### c. Xóa một node đã biết trước

Ở trên, chúng ta đã biết cách xóa đi node đầu và node cuối trong linked list, vậy còn mấy node ở giữa thì sao ?

Ở đây mình sẽ giả sử chúng ta cần xóa 1 node có data = x đi chẳng hạn. Kỹ thuật sử dụng vẫn là 2 con trỏ nhé.

```console
void deleteX(Node*& head, int x){
    if (head == nullptr){
        return ;
    }

    Node* cur = head ;
    Node* prev = nullptr ;
    
    while (cur != nullptr && cur -> data != x){
        prev = cur ;
        cur = cur -> next ;
    }

    if (cur == nullptr){
        return ;
    }

    if (prev == nullptr){
        head = head -> next ;
    }
    else {
        prev -> next = cur -> next ;
    }
    delete cur ;
}
```

Đầu tiên, như thường lệ, ta vẫn kiểm tra xem danh sách có rỗng kh, nếu rỗng thì trả về luôn

Tiếp theo, ta khởi tạo 2 con trỏ cur và prev. Sài cũng nhiều rồi nên chắc khỏi nói lại ha. Cách duyệt y chang [Thêm 1 node vào trước x](#a-thêm-1-node-vào-phía-trước-x) vậy.

Ở đây mình sẽ giả sử là xóa đi node có data là 60 nhé.

![](/img/linkedlist/deletemid1.png)

Lúc này, con trỏ cur đã tìm được node mang data là 60. Trường hợp không tìm dc thì cur == nullptr, lúc này ta return luôn vì kh tìm được node mà ta cần xóa.

```console
  if (prev == nullptr){
      head = head -> next ;
  }
  else {
      prev -> next = cur -> next ;
  }
  delete cur ;
```

Đầu tiên, ta kiểm tra con trỏ prev, nếu prev == nullptr, tức là node ta cần xóa đang ở vị trí đầu tiên (chính là head đó). Thì chúng ta chỉ việc thực hiện như [xóa node là head](#a-xóa-node-là-head) vậy.

Còn không, ta sẽ lấy prev -> next = cur -> next ;

Nhìn qua có vẻ khó hiểu ha, xem hình nha.

![](/img/linkedlist/prev->next=cur->next.png)
_prev -> next = cur -> next_

Ở đây, prev -> next chính là địa chỉ node mà cur đang nắm giữ đó (Ở đây là node 60). Còn cur -> next chính là địa chỉ của node sau cur (ở đây là node 10). 

Lật lại lý thuyết ban đầu một xíu nhé. Một node được cấu tạo từ phần data và con trỏ next. Trong đó, con trỏ next sẽ lưu trữ địa chỉ của node kế tiếp. Vì thế ta mới sử dụng cur -> next để lấy node kế tiếp sau node 60. Mục đích là tìm được node kế tiếp sau khi ta xóa đi node 60 đó.

Ta sẽ thực hiện gán cho prev -> next trỏ qua tới địa chỉ của node 10, bỏ qua node đang được con trỏ cur quản lý, vì mình đang cần xóa đi node cur mà.

Ta đã tạo được đường liên kết giữa node 30 và node 10. Công việc còn lại là xóa đi node 60 thôi.

![](/img/linkedlist/deletemidcur.png)

Vậy là xong rồi đó, chúng ta đã có thể xóa đi một node trong linked list.

Hmm, ở trên mình đã ví dụ cho trường hợp ta xóa đi node có giá trị là x rồi. Vậy thì sau khi đọc xong bài blog này, không biết các bạn có thể thực hiện: "Xóa đi một node thứ k trong linked list không ha". Không khó lắm đâu hehee.

> Bài test nho nhỏ : Xóa đi node thứ k trong linked list
{: .prompt-info }

### 5. Giải phóng linked list

Vì mỗi node trong linked list đều được ta cấp phát bộ nhớ. Cho nên, sau khi sử dụng xong, ta phải giải phóng chúng. Đây là một bước khá đơn giản nhưng nếu quên thì rất dễ gây ra nhiều hậu quả xấu cho chương trình như rò rỉ bộ nhớ,...

```console
void freeLinkedList(Node*& head){
    if (head == nullptr){
        return ;
    }
    else {
        Node* temp = head ;
        head = head -> next ;
        delete temp ;
    }
}
```

### 6. In linked list

Phần này cũng dễ nếu nãy giờ bạn đã nắm vững cách duyệt qua các phần tử trong linked list

```console
void printLinkedList(Node* head){
    Node* temp = head ;
    while (temp != nullptr){
        cout << temp -> data <<" ";
        temp = temp -> next ;
    }
}
```

## Lời kết

Qua bài blog này hi vọng các bạn có thể nắm những kiến thức cơ bản nhất của linked list - cũng là hành trang sau này để tiếp tục học các cấu trúc dữ liệu khác khó nhằn và phức tạp hơn trong tương lai. Vì cái DSA này chưa bao giờ là dễ cả =))))))

Thank you so much 

## Các nguồn tài liệu tham khảo

[Danh sách liên kết đơn trong C++](https://topdev.vn/blog/danh-sach-lien-ket-don-trong-c/)

[Series CTDL&GT - Linked List](https://www.youtube.com/watch?v=XduwHI8bbcA)

[Cấu trúc dữ liệu & Giải thuật: Linked List - Danh sách liên kết](https://www.youtube.com/watch?v=gzVTutcs3TY&t=1346s)

[Linked Lists for Technical Interviews - Full Course](https://www.youtube.com/watch?v=Hj_rA0dhr2I&t=161s)

Sách Kĩ Thuật Lập Trình - Trường ĐH KHTN - ĐHQG - HCM

________________

_Cừn_
