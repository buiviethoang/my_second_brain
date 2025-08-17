- jdbc, jpa
```
1, Dùng xong ko đóng connection. Hoặc đóng ko phải ở finally => khi hệ thống chay bt ko sao. Exception lâu sẽ leak connection

2. Chỗ thì dùng jpa, chỗ thì jdbc template, chỗ thì thuần ko đồng nhất

3. Dùng jdbctemplate nó đóng hộ connection. Tuy nhiên khi đó nêu trong hàm n lệnh db. Thì mỗi lệnh lại dùng connection riêng. Thành ra trong cùng 1 hàm wait connection rất nhiều lần. Và trong cả project bị blocking lẫn nhau nhiều nên chậm. 
=> phải open connection và dùng nó xuyên suốt hàm đó
=> nhiều ông kinh nghiệm cũng kém cái này vì phó mặc cho framework!

4.  Trong hàm sau khi mở conection db. Chưa đóng thì lại gọi rest api. Thành ra connection bị keep rất lâu. Không dc phép xử lý như thế
```

- diagram trong code