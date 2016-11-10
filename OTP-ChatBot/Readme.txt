nc chatbot.svattt.org 5555

Ask chatbot for the flag.

Source: chatbot.py


hint 1: https://eprint.iacr.org/2011/388.pdf section 3.1
hint 2: rsa is actually crt over 2 big primes, but it isn't restricted to only 2. also note that flag^d is independent from modulo, finally, we only need to consider small prime factors. good luck


Cứ mỗi lần kết nối thì mình lại nhận được 1 encrypt_key khác nhau 
"elif 'hello' in msg or 'hi' in msg or 'good' in msg or 'chao' in msg:
        res = greet[random.randrange(0,len(greet))]"
Mình gửi đến server vs message = “hi” để nhận về lại các enc  tương ứng với các greet của đề nhưng mà ở đây lại có 1 hàm random vì vậy mình gửi lên nhiều lần để nhận hết được tất cả các enc(greet[]) :D
Vì len(greet) = 4
Để tìm được encrypt_key  mình gcd 4 cái với d = 0x10001: 

(greet[0]^d – enc(greet[0]), greet[1]^d - enc(greet[1]), greet[2]^d - enc(greet[2]), greet[3]^d - enc(greet[3]))

Nhưng vì "res = greet[random.randrange(0,len(greet))]" ta ko thể biết được chính xác đâu là enc([greet[0,1,2,3]) vì vậy mình bruteforce => encrypt_key 

for (a,b,_c,d) in list(permutations(enc_list, 4)):
    temp = biggcd(c[0] -a, c[1] - b, c[2] - _c, c[3] -d )
    possible_encrypt_key.append(temp)

Lúc này mình sẽ tìm dc encrypt_key. 											   
Sau đó mình gửi FLAG? Đến server và nhận về được 1 đoạn enc1 = flag của đề bài
  
  "if 'FLAG?' in msg:
        res = FLAG"

Mình lại gửi tiếp FLAG? Đến server và cũng nhận được 1 đoạn enc2 = flag của đề bài

Bởi vì encrypt_key là random, nên factor có lúc được lúc không , cho nên mình sẽ gửi nhiêu lần, sau vài chục lần thử  factor encrypt_key ,thật sự lúc này rất nản và cũng gần hết giờ nhưng rất may cuối cùng lại tìm thấy đoạn có thể factor dễ dàng kaka, có các prime, mình tính phi và private key, sau đó decrypt `enc` là ra flag. SVATTT{CRT_CRT_CRT_101!!!!}

Ps: 2 bài crypto còn lại betacaro và chess các bạn có thể hoàn toàn giải được bằng tay.
    Bài betacaro khi kết nối vào server sẽ hỏi các bạn là chọn yes hay no để được đánh trước. Nếu chọn no server sẽ đánh trước và gửi cho các bạn một đoạn mã,đoạn mã đó biểu thị vị trí của điểm mà server đã đánh. chúng ta sẽ lấy mã này lại sau đó lại dùng đoạn mã này gửi lên server thì server sẽ gửi cho chúng ta một đoạn mã khác tương ứng với vị trí khác. chúng ta có thể làm theo cách này nhiều lần và lấy được các mã khác nhau tương ứng với các vị trí trong khung chơi sau đó dùng nó để chơi với server thôi. Có rất nhiều cách để giải quyết bài này, nhưng mình lại làm theo cách dễ nhất vì mình nghĩ nó rất vui và làm giảm bớt được những áp lực lúc thi.
    Bài chess, mình không nghĩ bài 250 điểm lại có thể dễ dàng như vậy, các bạn chỉ cần đi ngược ô e7e6 là giải quyết được vấn đề.Mình nghĩ bài này có thể bị lỗi hoặc ban tổ chức đã cố tình để vậy. Nhưng mình trong lúc thi cũng không nhận ra được vấn đề này,cứ nghĩ bài này rất khó nên đã không làm, khi về nhà làm ra mới thấy tiếc. 
