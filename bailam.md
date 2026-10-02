Câu 1: Phân biệt Value Types và Reference Types trong C#
Trong C#, Value Types là kiểu dữ liệu mà biến lưu trực tiếp giá trị. Khi gán một biến Value Type cho biến khác thì giá trị sẽ được sao chép sang biến mới. Một số kiểu thường gặp như int, double, bool, struct, enum.

Ví dụ:
int a = 10;
int b = a;
b = 20;

Lúc này a vẫn bằng 10 vì b chỉ nhận bản sao của giá trị a.
Còn Reference Types thì biến không lưu trực tiếp đối tượng mà lưu tham chiếu đến đối tượng. Đối tượng thường được tạo trên vùng nhớ Heap. Khi gán hai biến Reference Type cho nhau thì hai biến có thể cùng tham chiếu đến một đối tượng.

Ví dụ:
Student sv1 = new Student();
Student sv2 = sv1;

Lúc này sv1 và sv2 cùng tham chiếu đến một đối tượng Student.
Về vùng nhớ thì có thể hiểu đơn giản là Value Type thường được lưu trên Stack đối với biến cục bộ, còn đối tượng của Reference Type thường nằm trên Heap. Biến tham chiếu chỉ giữ địa chỉ tham chiếu đến đối tượng đó.

Câu 2: Init-only Properties (init) khác gì so với set?
set cho phép thay đổi giá trị của thuộc tính sau khi đối tượng đã được tạo.

Ví dụ:
Student sv = new Student();
sv.Name = "Minh";
sv.Name = "Nam";

Ở đây Name có thể thay đổi nhiều lần.
Còn init chỉ cho phép gán giá trị cho thuộc tính trong lúc khởi tạo đối tượng. Sau khi khởi tạo xong thì không thể thay đổi nữa.

Ví dụ:
class Student
{
    public string StudentId { get; init; }
    public string Name { get; set; }
}

Khi tạo đối tượng:

Student sv = new Student
{
    StudentId = "SV001",
    Name = "Minh"
};

Sau đó có thể thay đổi Name, nhưng không thể thay đổi StudentId.
init có thể sử dụng trong những trường hợp dữ liệu chỉ cần thiết lập một lần, ví dụ như mã sinh viên, mã sản phẩm hoặc ngày tạo đối tượng.

Câu 3: Phân biệt virtual và override

virtual được khai báo ở lớp cha, dùng để cho phép phương thức đó được lớp con ghi đè.
Còn override được khai báo ở lớp con để viết lại cách thực hiện của phương thức virtual ở lớp cha.

Ví dụ:

class Animal
{
    public virtual void Sound()
    {
        Console.WriteLine("Dong vat phat ra am thanh");
    }
}
class Dog : Animal
{
    public override void Sound()
    {
        Console.WriteLine("Cho sua gau gau");
    }
}
Khi thực hiện:

Animal a = new Dog();
a.Sound();
Kết quả sẽ là:
Cho sua gau gau
Điều này thể hiện tính đa hình. Mặc dù biến a có kiểu Animal nhưng đối tượng thực tế được tạo là Dog, nên phương thức Sound() của Dog được gọi.
Như vậy:
virtual dùng ở lớp cha để cho phép ghi đè.
override dùng ở lớp con để ghi đè phương thức của lớp cha.

Câu 4: Tại sao thành phần static không truy xuất thông qua Object Instance?

Thành phần được khai báo static là thành phần thuộc về lớp chứ không thuộc riêng về một đối tượng nào.

Ví dụ:

class Student
{
    public static int Count = 0;
}
Có thể truy cập Count bằng tên lớp:
Student.Count++;
Không cần phải tạo đối tượng bằng new.
Trong khi đó, nếu tạo:
Student sv = new Student();
thì sv chỉ là một đối tượng cụ thể của lớp Student. Thành phần static lại dùng chung cho cả lớp nên không gắn với riêng đối tượng sv.

Ví dụ:

Student sv = new Student();
Student.Count++;
Ở đây Count phải được gọi thông qua Student, còn những thuộc tính thông thường của đối tượng thì gọi thông qua sv.
Có thể hiểu đơn giản là:
Thành phần bình thường: thuộc về từng đối tượng → gọi bằng tên đối tượng.
Thành phần static: thuộc về cả lớp → gọi bằng tên lớp.
Vì vậy, thành phần static không được truy xuất theo cách thông thường thông qua Object Instance mà nên truy xuất trực tiếp bằng tên lớp.
