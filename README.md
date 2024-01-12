# revert-a-faulty-merge

Current resolution:
- Revert merge
- Continue developing on feature branch
- Merge feature branch back to development
- Missing old commits of the feature branch!

merge: Hợp Nhất
revert: Hoàn Nguyên
revert-a-faulty-merge: Hoàn Nguyên Một Hợp Nhất Không Đúng

Tôi có một nhánh chính. Chúng tôi có một nhánh phụ chia ra từ đó mà một số nhà phát triển đang làm việc. Họ cho rằng nó đã sẵn sàng. Chúng tôi hợp nhất nó vào nhánh chính. Nó làm hỏng một cái gì đó, nên chúng tôi hoàn nguyên hợp nhất. Họ thực hiện thay đổi vào mã nguồn. Họ đưa nó đến một điểm mà họ nói đó là ổn và chúng tôi lại hợp nhất.

Khi kiểm tra, chúng tôi phát hiện rằng các thay đổi mã nguồn được thực hiện trước khi hoàn nguyên không có trong nhánh chính, nhưng các thay đổi mã nguồn sau đó lại có trong nhánh chính.


* Commit 1
* * Commit 1a
* * Commit 1b
* * Commit 1d
* Commit 2
* Commit 3