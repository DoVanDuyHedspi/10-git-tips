# 10 mẹo để đẩy kĩ năng git của bạn lên cấp độ 
Gần đâu chúng tôi đã phát hành hai hướng dẫn để giúp bạn làm quen với [Git căn bản](http://www.sitepoint.com/git-for-beginners/)
và [Sử dụng git trong môi trường nhóm]. Những câu lệnh chúng ta đã bàn luận là đủ để giúp một nhà phát triển tồn tại được
trong thế giới Git. Trong bài đăng này, chúng ta cố gắng để khám phá xem làm thế nào quản lý
giời gian của bạn hiệu quả và tận dụng các tính năng mà git cung cấp.

Chú ý: Một vài câu lệnh trong bài báo này có một phần nằm trong dấu ngoặc vuông (ví dụ `git add -p [file_name]`).
Trong những ví dụ, bạn sẽ chèn số, định danh,.. cần thiền ở ngoài dấu ngoặc vuông.
## 1.Git tự hoàn thiện
Nếu bạn chạy câu lệnh Git thông qua dòng lệnh, thì đó là một nhiệm vụ mệt mỏi để gõ các lệnh
bằng tay mỗi lần. Để giúp đỡ điều đó, bạn có thể kích hoạt tự động hoàn thành các lệnh Git trong
vài phút.

Để có được kịch bản, hãy chạy lệnh sau trong một hệ thống Unix.

```
cd ~
curl https://raw.github.com/git/git/master/contrib/completion/git-completion.bash -o ~/.git-completion.bash
```
Tiếp theo, thêm những dòng lệnh sau vào file `~/.bash_profile` của bạn
```
if [ -f ~/.git-completion.bash ]; then
    . ~/.git-completion.bash
fi
```
Mặc dù tôi đã đề cập đến điều này trước đó, tôi không thể nhấn mạnh đủ: Nếu bạn muốn sử dụng các tính năng của Git đầy đủ,
bạn chắc chắn nên chuyển sang giao diện dòng lệnh!
## 2.Loại bỏ các file trong Git
Bạn có mệt mỏi với những file biên dịch (giống như `.pyc`) xuất hiện trong repo Git của bạn.
Hoặc rất chán khi bạn đã thêm nó vào Git?. Không cần tìm đâu xa, có một cách để ban có thể nói với
Git để hoàn toàn bỏ qua những thư mục và file. Đơn giản tạo một file có tên `.gitignore` và
và ghi danh sách các file và thư mục bạn không muốn Git theo dõi. Bạn có thể tạo các ngoài lệ bằng
dấu chấm than.
```
*.pyc
*.exe
my_db_config/

!main.pyc
```
## 3.Ai đã làm bẩn code của tôi?
Bản năng của con người là đổ lỗi cho người khác khi có điều gì đó sai. Nếu máy chủ production
bị phá vỡ, rất đơn giản để tìm thủ phạm - chỉ với `git blame`. Dòng lệnh này chỉ cho bạn tác giả
của tất cả dòng lệnh trong file, commit chỉ cho bạn thay đổi cuối cùng trong dòng lệnh đó, và thời
gian của commit.
```
git blame [file_name]
```
![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946443git-ninja-01.png)

Và trong ảnh chụp màn hình phía dưới, bạn có thể nhìn dòng lệnh đó sẽ trông như thế nào trong
repo lớn hơn.
![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946441git-ninja-02.png)


## 4.Xem lại lịch sử của Repository
Chúng ta đã được nhìn thấy việc sử dụng `git log` trong một hướng dẫn trước, tuy nhiên,
có ba lựa chọn mà bạn nên biết.
- `--oneline` - nén thông tin hiển thị bên cạnh mỗi commit với một commit giảm bớt và thông điệp
commit, tất cả nằm trên một dòng.
- `--graph` - Tùy chọn này vẽ ra một biểu diễn đồ thị dựa trên văn bản của lịch sử ở phía bên tay trái của đầu ra. 
Không sử dụng nếu bạn đang xem lịch sử cho một nhánh đơn.
- `--all` - đưa ra lịch sử tất cả các nhánh.

Dưới đây là những gì kết hợp các tùy chọn trông giống như

![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946444git-ninja-03.png)

## 5.Không bao giờ theo dõi xót một commit
Hãy nói bạn đã commit một điều gì đó mà bạn không muốn và kết thúc bằng cách cố gắng thiết lập
lại trạng thái trước đó của bạn. Một lúc sau, bạn nhận ra đã mất một vài thông tin trong quá 
trình và muốn quay lại hoặc ít nhất là xem nó. Đây là lúc `git reflog` có thể giúp.

Đơn giản `git log` đưa cho bạn xem commit cuối, cha của nó, cha của cha nó, vân vân.
Tuy nhiên, `git reflog` là một danh sách commit mà cái đứng đầu được chỉ đến. Nhớ rằng nó 
thuộc về hệ thống của bạn, nó không là một phần của repo và không bao gồm pushes và merges.

Nếu tôi chạy `git log`, tôi sẽ nhận được những commit nằm trong repo.

![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946446git-ninja-04.png)

Tuy nhiên, một `git reflog` đưa ra một commit (**b1b0ee9 – HEAD@{4}**) đã bị mất khi bạn
cố gắng cài lại.
![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946447git-ninja-05.png)
 