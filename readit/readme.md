bây giờ minh xin viết lại write câu for 150 Readit SVATTT 2016
</br>
hint: checksum
</br>
trước tiên bật "Validate the TCP checksum if possible" (Edit->Preferences..->Protocols->TCP-> Validate the TCP checksum if possibl)
bạn thấy checksum [incorrect,....]
</br>
![readit](https://cloud.githubusercontent.com/assets/23380906/20177836/60d0b8d2-a781-11e6-9e2b-7f309bbe1ce6.png)

</br>
0x88 - 0x65 = 0x23
</br>
data = 0x30
</br>
flag : chr(0x30+0x23) = 'S'
</br>
0xa6 - 0x62 = 0x44
</br>
data = 0x12
</br>
flag : chr(0x12+0x44) = 'V'
</br>
.....
</br>
....
</br>
flag : SVATTT{s0_now_y0u_know_h0w_T0_c4lcul@t3_tcp_chk5um}
