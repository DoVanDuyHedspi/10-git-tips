# 10 mẹo để đẩy kĩ năng git của bạn lên cấp độ 
Gần đâu chúng tôi đã phát hành hai hướng dẫn để giúp bạn làm quen với [Git căn bản](http://www.sitepoint.com/git-for-beginners/)
và [Sử dụng git trong môi trường nhóm]. Những câu lệnh chúng ta đã bàn luận là đủ để giúp một nhà phát triển tồn tại được
trong thế giới Git. Trong bài đăng này, chúng ta cố gắng để khám phá xem làm thế nào quản lý
giời gian của bạn hiệu quả và tận dụng các tính năng mà git cung cấp.

Chú ý: Một vài câu lệnh trong bài báo này có một phần nằm trong dấu ngoặc vuông (ví dụ `git add -p [file_name]`).
Trong những ví dụ, bạn sẽ chèn số, định danh,.. cần thiền ở ngoài dấu ngoặc vuông.
## 1. Git tự hoàn thiện
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
## 2. Loại bỏ các file trong Git
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
## 3. Ai đã làm bẩn code của tôi?
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


## 4. Xem lại lịch sử của Repository
Chúng ta đã được nhìn thấy việc sử dụng `git log` trong một hướng dẫn trước, tuy nhiên,
có ba lựa chọn mà bạn nên biết.
- `--oneline` - nén thông tin hiển thị bên cạnh mỗi commit với một commit giảm bớt và thông điệp
commit, tất cả nằm trên một dòng.
- `--graph` - Tùy chọn này vẽ ra một biểu diễn đồ thị dựa trên văn bản của lịch sử ở phía bên tay trái của đầu ra. 
Không sử dụng nếu bạn đang xem lịch sử cho một nhánh đơn.
- `--all` - đưa ra lịch sử tất cả các nhánh.

Dưới đây là những gì kết hợp các tùy chọn trông giống như

![image](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946444git-ninja-03.png)

## 5. Không bao giờ theo dõi xót một commit
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
 
## 6. Phân loại các phần của một tệp đã thay đổi cho một commit
Nói chung đây là một thủ tục tốt để thực hiện các commit dựa trên tính năng, đó là mỗi một 
commit phải đại diện cho một tính năng hoặc sửa lỗi. Cân nhắc điều gì sẽ xảy ra nếu bạn sửa
hai lỗi hoặc thêm nhiều tính năng mà không thay đổi commit. Trong hoàn cảnh tình hình như
vậy, bạn có thể đẩy sự thay đổi vào một commit đơn. Nhưng có một các tốt hơn: Xếp các tập tin riêng lẻ và
 commit chúng một cách riêng biệt.
 
 Hãy nói bạn đã tạo ra nhiều thay đổi trong một file đơn và muốn chúng xuất hiện trong các
 commit tách riêng. Trong trường hợp này, chúng ta thêm các tập tin bằng tiền tố `-p` vào các lệnh thêm của
  chúng ta.
  
  ```
  git add -p [file_name]
  ```
  Chúng ta hãy cùng nhau chứng minh. Tôi đã thêm ba dòng mới vào `file_name` và chỉ muốn 
  dòng thứ nhất và thứ ba xuất hiện trong commit. Hãy xem `git diff` đưa ra chúng:
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946449git-ninja-06.png)
  
  Và xem điều gì sẽ xảy ra khi chúng ta thêm tiền tố `-p` vào lệnh `add` của chúng ta.
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946450git-ninja-07.png)
  
  Dường như Git cho rằng tất cả những thay đổi đều là một phần của cùng một ý tưởng,
  do đó nhóm nó vào một nhóm lớn đơn lẻ. Bạn có các lựa chọn:
  
  - Gõ y để stage nhóm đó
  - Gõ n để không stage nhóm đó
  - Gõ e để sửa nhóm đó thủ công
  - Gõ d để thoát hoặc đi tới tệp tiếp theo
  - Gõ s để chia tách nhóm
  
  Trong trường hợp của chúng ta, chúng ta chắc chắn muốn tách nó thành từng phần nhỏ để thêm
  một số và bỏ qua phần còn lại.
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946452git-ninja-08.png)
  
  Như bạn có thể thấy, chúng ta đã thêm dòng thứ nhất và thứ ba và bỏ qua dòng thứ hai.
  Bạn có thể tiếp tục xem trạng thái của repo và tạo một commit.
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946454git-ninja-09.png)
  
  ## 7. Nén nhiều commit
  Khi bạn gửi đi code của bạn để xem lại và tạo một pull request(mà thường xảy ra trong các dự án nguồn mở )
  bạn có thể được yêu cầu thực hiện thay đổi cho mã của mình trước khi nó được chấp nhận.
  Bạn thực hiện thay đổi, chỉ để được yêu cầu thay đổi lại nó trong lần xem xét tiếp theo.
  Trước khi bạn biết điều đó, bạn có một vài commit thêm. Lý tưởng nhất, bạn có thể nén chúng vào 
  một bằng cách sử dụng lệnh `rebase`.
  
  ```
  git rebase -i HEAD~[number_of_commits]
  ```
  
  Nếu bạn muốn nén 2 commit cuối, lệnh bạn chạy như sau.
  
  ```
  git rebase -i HEAD~2
  ```
  Trong câu lệnh chạy, bạn được đưa đến một giao diện tương tác liệt kê các commit và yêu 
  cầu bạn những commit nào để nén.
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946455git-ninja-10.png)
  
  Sau đó bạn được yêu cầu cung cấp thông báo commit cho commit mới. Quá trình này chủ yếu viết 
  lại lịch sử commit của bạn.
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946457git-ninja-11.png)
  
  ## 8. Cất những thay đổi chưa được commit
  Hãy nói rằng bạn đang làm việc với một lỗi nhất định và một tính năng, và bạn
  đột nhiên được yêu cầu mô tả công việc của bạn. Công việc hiện tại chưa đủ hoàn thiện
  để commit, và bạn không thể đưa ra một mô tả trong giai đoạn này(mà không cần quay lại
  các thay đổi). Trong trường hợp như vậy, `git stash` trở thành cứu tinh. Stash thực sự có tất cả các thay đổi của bạn 
  và lưu trữ chúng để sử dụng thêm. Để giấu các thay đổi của bạn, bạn chỉ cần chạy lệnh sau
  
  ```
 git stash 
  ```
  
 Để kiểm tra danh sách stashes, bạn có thể chạy như sau:
 
 ```
 git stash list
 ```
 
 ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946458git-ninja-12.png)
 
 Nếu bạn muốn un-stash và phục hồi các thay đổi không bị giam, bạn áp dụng các stash:
 
 ```
 git stash apply
 ```
 
 Trong ảnh chụp màn hình cuối, bạn có thể thấy rằng mỗi stash có một  indentifier, một số duy nhất 
 (mặc dù chúng ta chỉ có một stash trong trường hợp này)
 
  ```
git stash apply stash@{2}
  ```
  
  ![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946461git-ninja-13.png)
  
  ## 9. Kiểm tra những commit bị mất
  Mặc dù `reflog` là một cách để kiểm tra các commit bị mất, nó không khả thi trong một
  repo lớn. Đó là khi lệnh `fsck` (kiểm tra hệ thống tập tin) xuất hiện.
  
```
 git fsck --lost-found
```

![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946463git-ninja-14.png)

Ở đây bạn có thể thấy một commit bị mất. Bạn có thể kiểm tra những thay đổi trong commit 
bằng cách chạy `git show [commit_hash]` hoặc khôi phục lại nó bằng cách chạy `git merge [commit_hash]`.

`git fsck` có một lợi thế hơn `reflog`. Hãy nói răng bạn đã xóa một remove branch và sau đó
clone repo. Với `fsck` bạn có thể tìm khôi phục lại remove branch đã xóa.

## 10. Cherry Pick
Cuối cùng tôi đã lưu lại các câu lệnh Git tao nhã nhất. Câu lệnh ```cherry-pick` là câu lệnh Git ưa thích nhất của tôi, bởi vì ý nghĩa thực cũng như tính hữu dụng của nó!

Với những giới hạn đơn giản nhất, ```cherry-pick``` sẽ chọn 1 commit đơn lẻ từ các nhánh khác nhau và hợp chúng với cái hiện tại. Nếu bạn đang làm việc theo cách song sóng trên 2 hay nhiều hơn nhánh, bạn có thể chú ý 1 lỗi mà xuất hiện ở tất cả các nhánh. Nếu bạn giải quyết nó trong 1, bạn có thể cherry pick commit đến cácnhánh khác, mà không làm rỗi loạn với các file hay commit khác


Hãy hình dung 1 kịch bản khi bạn có thể gọi nó. Tôi có 2 nhánh và tôi muốn ```cherry-pick``` commi ts```b20fd14: Cleaned junk``` đến 1 nhánh khác
![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946465git-ninja-15.png)

Tôi chuyển tới nhánh tới nhánh tôi muốn ```cherry-pick``` commit, và chạy lệnh sau
```

git cherry-pick [commit_hash]

```

![img](https://dab1nmslvvntp.cloudfront.net/wp-content/uploads/2014/06/1402946467git-ninja-16.png)

Mặc dù lần này tôi đã dọn ```cherry-pick```, bạn nên biết rằng cây lệnh này thường dẫn tới các xung đột, vì vậy sử dụng nó cẩn thận.

## Kết luận

Với những điều này, chúng tôi đi đến kết luận của danh sách các lời khuyên của chúng tôi mà tôi nghĩ rằng có thể giúp bạn nâng tầm các kĩ năng Git của ban. Git là thứ tốt nhất ngoài đó và nó có thể  hoàn thành bất cứ thứ gì mà bạn có thể tưởng tượng. Vìì thế, hãy luốn cố gắng thách thức bản thân với Git. Cơ hội đến, bạn sẽ có thể học được điều gì đó mới mẻ!

