2025-08-30 09:34
Status: #baby
Tags: [[productivity]]
## Main

**Bạn clone code từ main về nhưng muốn làm việc tại nhánh khác. Tuy nhiên, bạn đã chỉnh sửa 1 đoạn code từ main. Giờ bạn muốn move tất cả code từ main sang nhánh đó để work locally với nó. How to?**
Answer: Bạn sử dụng `git checkout old_branch` để tạm biệt branch cũ 
Tiếp đó dùng lệnh `git branch new_branch` để tạo nhánh mới.
Cuối cùng là `git checkout new_branch` để chuyển tất cả code của nhánh cũ sang nhánh mới 
**Bạn có một đám code cần add vào stage. Bạn muốn add tất cả cho nhanh nhưng lại gặp 1 vấn đề là có nhiều file có trong .gitignore và không thể add cùng được. Bạn làm thế nào để vẫn add các file khác mà không add các file ignored đó?**
Answer: Sử dụng `git reset name_of_file` để phục hồi trạng thái cho code (unstaged) và sau đó `git add .` để add tất cả các file còn lại.

**Bạn trót commit nhầm lên git 1 vài commit (cố gắng commit để sửa sai nhưng éo được". Giờ đây bạn muốn trở về những trạng thái commit cũ. Bạn phải làm như nào?**
Answer: 
Sử dụng `git reset --hard HEAD~num_of_commit` 
**Trong trường hợp bạn chỉ muốn xóa 1 file trong cái commit bạn vừa mới commit nhầm ấy. Chỉ có file ấy lỗi thôi, còn lại ổn. Bạn làm như nào? **
`git reset --soft HEAD~1` 
Sau đó thì 
`git restore --staged file_to_remove` 
Và commit lại thôi. 
*num_of_commit ám chỉ số commit trong log từ mới nhất dật về xa. Nếu là 3 thì sẽ xóa đi 3 commit gần nhất*
**Bạn muốn push một số file lên git. Tuy nhiên trong đám file đó có 1 file rất nặng (> 100MB). Github bản free có vẻ như ko cho phép bạn push quá 100MB lên repo. Do đó bạn phải remove file đó đi và ko push file đó lên nữa. Vấn đề là nếu bạn chỉ xóa đi ở local đến khi commit thì git vẫn nhớ cái file đó. Giờ bạn phải tìm cách cho git hiểu là file đó đã bị remove khỏi commit? How?**
Anwer: Bạn làm như sau:
```shell
$ git rm --cached giant_file
# Stage our giant file for removal, but leave it on disk
```
```shell
$ git commit --amend -CHEAD
# Amend the previous commit with your change
# Simply making a new commit won't work, as you need
# to remove the file from the unpushed history as well
```
```shell
$ git push
# Push our rewritten, smaller commit
```

**Bạn vừa mới reset 1 commit. Giờ bạn thấy hối hận. Bạn muốn go back to cái commit mới nhất mà bạn vừa reset đó. How?**
`git reflog` để xem hết những cái gì bạn thao tác (nó gọi là ref updates) chứa checkout, reset, commit, merge. 	
Ở trong cái log này bạn sẽ thấy được một vài thứ như sau: 
```
$ git reflog
3f6db14 HEAD@{0}: HEAD~: updating HEAD
d27924e HEAD@{1}: checkout: moving from d27924e0fe16776f0d0f1ee2933a0334a4787b4c
[...]
```
bạn sẽ nhìn thấy những gì bạn đã thao tác. 
Để undo 1 vài thao tác (lấy lại code) bạn chỉ cần làm như sau:
`git reset 'HEAD@{1}'` nếu bạn muốn lấy lại cái commit ở vị trí HEAD@{1}
Nếu bạn muốn định rõ branch nào bạn muốn nhìn thấy log
```
$ git reflog show master
```
**Bạn muốn remove những untracked file ?**
- Step 1 is to show what will be deleted by using the `-n` option:
```
# Print out the list of files and directories which will be removed (dry run)
git clean -n -d
```
- Clean Step - **beware: this will delete files**:
```
# Delete the files from the repository
git clean -f
```
 -   To remove directories, run `git clean -f -d` or `git clean -fd`
 -   To remove ignored files, run `git clean -f -X` or `git clean -fX`
 -   To remove ignored and non-ignored files, run `git clean -f -x` or `git clean -fx`

**Bạn muốn chỉnh sửa lại 1 vài chi tiết trong commit trước? How?**
Answer: Dùng `git commit --amend`

***Cái này phải chú ý này: Khi bạn vừa commit trên local. Bạn đẩy nó lên remote bằng cách push. Giờ bạn thấy cái commit đấy sai vl. Bạn cố gắng sửa ở local với những cái commit khác (tất nhiên có sửa file). Giờ đây bạn push ngược lên thì rõ ràng thằng remote nó không nhận. Giờ hoặc là bạn phải pull ngược từ remote về rồi stash cái local rồi mới push ngược lại lên. Như thế thì số dòng code nó sẽ tăng nhiều lắm. Bạn chọn phương án 2: Quay ngược thằng remote về previous commit của nó. Cái này bạn phải làm như nào?***
Answer: Bạn dùng như sau:
`git reset --hard <commit>`
`git push -f origin`
Bây giờ thì thằng remote nó sẽ nhận lại cái push trước đó của bạn. 

**Bạn muốn commit code lên github. Nhưng thằng đĩ đồng nghiệp nó push lên 1 vài commit lên cùng cái nhánh upstream đó mất rồi. Giờ bạn push lên mà git nó cứ báo lỗi và ko cho bạn push. Bạn phải làm thế nào?**
Bạn có một vài cách sau: 
- Bắt nó push anyway. Cách này cũng được. Bạn có thể tự tin cho rằng mình đúng và fuckings care code trên github nó như nào. Cứ thế mà push thẳng lên thôi, chả cần phải lấy cái update của thằng bạn của bạn. Nếu thế thì bạn dùng cái này: 
`git push -f` xong phim! 
- Bạn cẩn trọng hơn, tôn trọng những cập nhật từ phía đồng nghiệp. Bạn phải làm thế nào? 

## References
