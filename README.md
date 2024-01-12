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
* * Commit 1c
* * Commit 1d
* Commit 2
* Commit 3


Lịch sử ngay sau "hoàn nguyên hợp nhất" sẽ trông như sau:

---o---o---o---M---x---x---W
               /
       ---A---B (feat/wav-1)

Sau khi các nhà phát triển của nhánh phụ (feat/wav-1) sửa chữa lỗi của họ, lịch sử có thể trông như sau:


---o---o---o---M---x---x---W---x--------M2 (main)
               /                       /
       ---A---B-------------------C---D (feat/wav-1)

Việc "hoàn nguyên" một commit thường chỉ đơn giản là làm ngược lại những gì commit đó đã làm, và khá đơn giản. Nhưng việc "hoàn nguyên" một commit hợp nhất cũng làm ngược lại dữ liệu mà commit đó đã thay đổi, nhưng nó không làm gì cả với lịch sử mà commit hợp nhất đã có.

Vì vậy, hợp nhất vẫn tồn tại, và nó vẫn được coi là sự kết hợp giữa hai nhánh, và các hợp nhất sau này vẫn nhìn thấy hợp nhất đó như là trạng thái chia sẻ cuối cùng - và hoàn nguyên đưa vào sẽ không ảnh hưởng gì cả.

Vì vậy, một "hoàn nguyên" hoàn nguyên lại những thay đổi dữ liệu, nhưng nó không phải là một "phục hồi" theo cách nó không hoàn nguyên tác động của một commit lên lịch sử kho chứa.


Với tình huống như vậy, bạn muốn trước hết hoàn nguyên "hoàn nguyên trước đó", khiến lịch sử trông như sau:

---o---o---o---M---x---x---W---x---Y (main)
               /
       ---A---B-------------------C---D (feat/wav-1)


Tuong tu nhu:
---o---o---o---M---x---x-------x-------*
               /                       /
       ---A---B-------------------C---D



Cach 2
 ---o---o---o---M---x---x---W---x---x
               /                 \
       ---A---B                   X' (squashed A, B, C, D)


Conflict
---o---o---o---M---x---x---W---x---x---Y---*
               /                 \         /
       ---A---B                   A'--B'--C'

C
B