# Git
## Git là gì?
- Git là công cụ quản lý các phiên bản của các tập tin (VCS - Version Control System) 
- Git cung cấp các chức năng như:
    + Lưu trữ các phiên bản của các tập tin
    + Theo dõi các thay đổi của các tập tin
    + Khôi phục các phiên bản cũ
    + Tạo các nhánh (branch) để phát triển các tính năng mới, làm việc độc lập với nhau.
    
![git common](screenshots/git-common.jpg)

Như hình trên, repository được lưu trên cloud.
Khi làm việc, thì ta sẽ không thao tác trực tiếp trên cloud, mà sẽ dùng git để clone về. Mục đích là nhiều người có thể đồng thời làm việc với repo này.
Lúc này ta có bản local của repository. Mô hình giống trên ảnh.
- Tuy nhiên, ta sẽ gặp vấn đề khi đẩy code lên lại repo cloud.
## Chúng ta cần phân biệt rõ ràng giữa repo cloud và repo local (Mối quan hệ)
- Repo cloud: là repo trên cloud, chứa các phiên bản của các tập tin, nơi nhiều người có thể làm việc đồng thời.
- Repo local: là repo trên máy tính cá nhân, chứa các phiên bản của các tập tin, nơi mà mỗi người làm việc độc lập.

- 1 repo - n repo local
- n repo local -> push -> 1 repo cloud

## Vấn đề khi đẩy code lên repo cloud
- Do mỗi repo local là độc lập, khi đẩy code lên 1 repo cloud, có tiềm ẩn khả năng gây ra xung đột (conflict) giữa các phiên bản của các tập tin. (Cùng người cùng sửa 1 dòng code), từ các commit cùng cấp.

![git conflict](screenshots/git-conflict.jpg)

- Để giải quyết vấn đề này, ta cần phải đồng bộ lại các phiên bản của clone 2 và repo cloud. Sau đó push lên với một phiên bản mới (commit mới).
- Đồng bộ lại các phiên bản của repo local và repo cloud, ta sẽ dùng lệnh `git pull` để lấy về các phiên bản mới nhất của repo cloud.
- Sau khi đồng bộ, ta sẽ dùng lệnh `git push` để đẩy code lên repo cloud.

![git conflict](screenshots/git-conflict-solve.jpg)

## Tại sao cần có các nhánh?
- Khi làm việc với repo cloud, ta sẽ không thao tác trực tiếp trên nhánh master, mà sẽ tạo ra các nhánh mới để làm việc. Sau khi hoàn thành, ta sẽ merge vào nhánh master.
- Dùng nhánh sẽ giúp ta đảm bảo tính toàn vẹn của nhánh master. Vì nhánh master chỉ được merge khi đã được kiểm tra kỹ lưỡng.
- Đồng thời branch giúp ta làm việc độc lập trên các chức năng khác nhau, giảm thiểu trường hợp `quá nhiều người cùng thao tác trên 1 nhánh`.

## Các lệnh cơ bản của git
- Trước khi vào các lệnh cơ bản, ta cần phải hiểu rõ ràng về các khái niệm sau:
    + repo: là thư mục chứa các tập tin, các phiên bản của các tập tin, chứa file .git
    + Commit: là một phiên bản của các tập tin, được lưu trữ trên repo local.
    + Branch: là một nhánh, được tạo ra từ một commit nào đó. Mỗi branch sẽ có một commit đặc biệt, được gọi là commit gốc (root commit).
    + Merge: là hành động gộp các commit của 1 branch vào branch khác.
    + Pull: là hành động lấy về các commit mới nhất của repo cloud.
    + Push: là hành động đẩy các commit lên repo cloud.
    + Checkout: là hành động chuyển đổi giữa các branch hoặc commit.
    + Rebase: là hành động gộp các commit của 1 branch vào branch khác, nhưng sẽ không tạo ra commit mới. (git pull --rebase)

- Ta chia ra được thành 5 mục nhỏ
    + Getting and Creating Projects
    + Basic Snapshotting
    + Branching and Merging
    + Sharing and Updating Projects
    + Patching
### Getting and Creating Projects
- `git init`: Khởi tạo một repo local
```bash
$ git init
```
- `git remote add origin <server>`: Thêm một remote repo
```bash
$ git remote add origin <server>
```
- `git clone <server>`: Clone một repo về máy
```bash
$ git clone <server>
```

### Basic Snapshotting
#### Các lệnh thưởng sử dụng
- `git status`: Kiểm tra trạng thái của repo
- `git add`: Thêm các tập tin vào staging area
```bash
$ git add <file>
or
$ git add .
~ thêm tất cả các tập tin
```
Ở đây sẽ đẻ ra các trạng thái của file:  (tùy từng trạng thái mà liên quan đến việc file này có được khôi phục lại hay không)

    + Untracked: là các file chưa được add vào staging area

![git untracked](screenshots/git-untracked.PNG)

    + Unmodified: là các file đã được add vào staging area, nhưng chưa được commit

![git unmodified](screenshots/git-unmodified.PNG)

    + Modified: là các file đã được commit, nhưng chưa được push lên repo cloud

![git modified](screenshots/git-modified.PNG)

    + Staged: là các file đã được commit, và đã được push lên repo cloud
    
![git staged](screenshots/git-staged.PNG)

```bash
Một số kí hiệu trong visual studio code
A - Added (This is a new file that has been added to the repository)
M - Modified (An existing file has been changed)
D - Deleted (a file has been deleted)
U - Untracked (The file is new or has been changed but has not been added to the repository yet)
C - Conflict (There is a conflict in the file)
R - Renamed (The file has been renamed)
S - Submodule (In repository exists another subrepository)
```

![git log](screenshots/git-stage.webp)

- `git commit`: Tạo một commit mới
```bash
$ git commit -m "message"
~ m ở đây là message, là một thông điệp mô tả cho commit
```

![git commit](screenshots/git-commit.PNG)

- `git log`: Hiển thị các commit đã được thực hiện
```bash
$ git log
```

![git log](screenshots/git-log.PNG)

Ngoài ra 
- `git diff`: Hiển thị các thay đổi giữa các commit
- `git reset`: Đưa các tập tin về trạng thái trước khi commit
- `git rm`: Xóa các tập tin khỏi repo
- `git mv`: Di chuyển các tập tin trong repo

### Branching and Merging
Đây là nhánh cây đầu tiên của repo. Nó chỉ gồm 1 nhánh duy nhất là mặc định là main.

![git log](screenshots/git-branch-1.PNG)

- `git branch`: Hiển thị các nhánh hiện có

![git branch](screenshots/git-branch.PNG)

- `git branch <branch-name>`: Tạo một nhánh mới ở local. Nhánh chỉ được tạo trên remote khi push lên repo cloud tại nhánh này.
```bash
$ git branch <branch-name>
```

![git branch](screenshots/git-branch-2.PNG)

Như vậy ta đã tạo thành công một nhánh mới là `main_B`. Cùng check lại các nhánh hiện có bằng lệnh `git branch`

![git branch](screenshots/git-branch-3.PNG)

Dấu `*` ở trước tên nhánh là nhánh ta đang ở.
Cùng check lại nhánh cây xem sao nhé!

![git branch](screenshots/git-branch-1.PNG)

Nhánh cây hiện tại vẫn như ban đầu, vì ta chưa push lên repo cloud.
Đây là nhánh cây sau khi ta push lên repo cloud tại nhánh `main_B`

![git branch](screenshots/git-branch-4.PNG)

Dấu đỏ mình khoanh tròn là nhánh `main_B` đã được push lên repo cloud. Do mình push lên với cùng commit của main nên trông 2 nhánh giống như 1 vậy.

- `git checkout <branch-name>`: Chuyển sang nhánh mới
```bash
$ git checkout <branch-name>
```

Tiếp đó mình sẽ thử thay đổi một số file để tạo ra commit mới. Sau đó push lên repo cloud tại nhánh `main_B`. Cùng check lại nhánh cây xem sao nhé!

![git branch](screenshots/git-branch-5.PNG)

Lúc này cây cây sẽ dài ra tiếp. Do nhánh `main_B` vẫn được phát triển từ `cm main`.

Tuy nhiên, khi ta chuyển lại sang nhánh main, ta sẽ không thấy được những thay đổi vừa thực hiện trên nhánh `main_B`. Cùng check lại xem sao nhé!

![git branch](screenshots/git-branch-6.PNG)

Lúc này ta sẽ thay đổi một số file trên nhánh `main` và push lên repo cloud. Cùng check lại nhánh cây xem sao nhé!

![git branch](screenshots/git-branch-7.PNG)

Lúc này cây đã được rẽ nhánh, do nhánh `main` và `main_B` có commit khác nhau và cùng phát triển từ commit `cm main`.

- `git branch -d <branch-name>`: Xóa một nhánh mới ở local.
```bash
$ git branch -d <branch-name>
```

![git branch -d](screenshots/git-branch-d.PNG)

- `git branch -D <branch-name>`: Xóa một nhánh mới ở local. (Dùng khi nhánh đó chưa được merge)
```bash
$ git branch -D <branch-name>
```

![git branch -D](screenshots/git-branch-De.PNG)

- `git push origin --delete <branch-name>`: Xóa một nhánh mới ở remote.
```bash
$ git push origin --delete <branch-name>
```

![before delete branch](screenshots/before-delete-branch.PNG)
![after delete branch](screenshots/after-delete-branch.PNG)

- `git checkout <file-name>`: Khôi phục lại file
```bash
$ git checkout <file-name>
```
- `git switch <branch-name>`: Chuyển sang nhánh mới. Cơ chế của thằng này giống hệt thằng `git checkout <branch-name>`.
```bash
```bash
$ git switch <branch-name>
```
- `git merge <branch-name>`: Merge nhánh mới vào nhánh hiện tại
```bash
$ git merge <branch-name>
```

![git merge](screenshots/git-merge.PNG)

Chúng ta sẽ thấy một số file bị conflict. Để xem file nào bị conflict, ta dùng lệnh `git status` . Lí do bị conflict là do 2 nhánh có thay đổi cùng một file tại cùng một dòng. Cùng check lại xem sao nhé!

![git merge](screenshots/git-merge-2.PNG)

Để khắc phục conflict, ta chỉnh sửa file đó theo ý mình. Sau đó add và commit như bình thường.

![git merge](screenshots/git-merge-3.PNG)

Lúc này nhánh cây sẽ chụm vào nhánh `main`.
Nếu ta chuyển sang nhánh `main_B` và commit thêm một số file, sau đó push lên repo cloud thì nhánh cây sẽ như này:

![git merge](screenshots/git-merge-4.PNG)

### Sharing and Updating Projects
- `git push`: Đẩy các commit lên repo cloud
- `git fetch`: Lấy các commit mới nhất từ repo cloud về local nhưng không tự động merge
- `git pull`: Lấy các commit mới nhất từ repo cloud về local và merge vào nhánh hiện tại
 Để hiểu rõ về 2 lệnh `git fetch` và `git pull` thì mình cùng xem ví dụ nhé!
 Mình sẽ tạo thêm 1 bản local khác của repo cloud. mình sẽ gọi bản này là `local2`. Mình sẽ thực hiện một số thay đổi trên `local2` và tạo ra tình huống conflict và push lên repo cloud. Lúc này thì `local1` sẽ không có những thay đổi đó. Do chưa được cập nhật lại từ repo cloud. Cùng check lại xem sao nhé!

![git fetch](screenshots/git-fetch.PNG)

Cùng thử lệnh `git fetch` trên `local1` xem sao nhé!

![git fetch](screenshots/git-fetch-2.PNG)

Lúc này thì `local1` đã được cập nhật lại từ repo cloud. Nhưng chưa được merge vào nhánh hiện tại và vẫn giữ nguyên ở commit hiện tại. Cùng check lại xem sao nhé!

![git fetch](screenshots/git-fetch-3.PNG)

Tuy nhiên khi ta muốn tạo thêm một commit mới thì sẽ đè lên commit mới nhất với dữ liệu cũ, lỗi này không được phép có trong project thực tế. Do vậy `git fetch` chỉ có tác dụng cập nhật thông tin, trạng thái repo.

![git fetch](screenshots/git-fetch-4.PNG)

Sau khi dùng `git pull` thì `local1` đã được cập nhật và merge nhánh mới vào nhánh hiện tại. Ở đây bị conflict thì ta xử lí như tình huống giống trên merge. 

![git pull](screenshots/git-pull.PNG)

`git pull` = `git fetch` + `git merge`

### Patching
- `git stash`: Lưu các thay đổi hiện tại vào một khu vực tạm thời
- Trước khi gọi lệnh `git stash` thì các thay đổi sẽ được hiển thị như sau:

![git stash](screenshots/git-stash.PNG)

- Sau khi gọi lệnh `git stash` thì các thay đổi sẽ được hiển thị như sau:

![git stash](screenshots/git-stash-2.PNG)

```bash
Lưu các thay đổi chưa được commit vào một khu vực tạm thời và xóa các thay đổi đó khỏi staging area
```
- `git stash pop`: Lấy các thay đổi đã lưu trước đó

![git stash](screenshots/git-stash-3.PNG)

```bash
Lấy các thay đổi đã lưu trước đó và merge vào nhánh hiện tại

Dùng git stash và stash pop khi git pull bị conflict.
$ git pull
 ...
file foobar not up to date, cannot merge.

$ git pull

D: problem solved
```
- `git rebase`: Dễ hiểu thì `git rebase` sửa đường nối của các commit.
from:      A---B---C topic
         /                 
    D---E---A'---F master
to:
                   B'---C' topic
                  /
    D---E---A'---F master
from:
    o---o---o---o---o  master
         \
          o---o---o---o---o  next
                           \
                            o---o---o  topic
to:
    o---o---o---o---o  master
        |            \
        |             o'--o'--o'  topic
         \
          o---o---o---o---o  next
Để hiểu rõ hơn thì các bạn có thể xem thêm tại [đây](https://git-scm.com/docs/git-rebase)

- `git revert`: Revert một commit
```bash
$ git revert <commit-id>
```
# Git flow