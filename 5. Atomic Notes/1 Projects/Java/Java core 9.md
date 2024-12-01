  ## Date and time API
  ### The Time Line
  - An instant represents a point on the time line. An origin, called the epoch is arbitrarily set at midnight Jan 1, 1970. 
  - Starting from that origin, time is measured in 86,400 seconds per day, forwards and backwards, to nanosecond precision
- The Instant values go back as far as a billion years (Instant.MIN). That's not quite enough to express the age of the Universe (around 13.5 billion years), but it should be enough for all practical purposes. After all, a billion years ago, the Earth was covered in ice and populated by microscopic ancestors of today’s plants and animals. The largest value, Instant.MAX, is December 31 of the year 1,000,000,000

The static method call **Instant.now()** gives the current instant

### LocalDates
Cái này khá là phổ biến, và cần phân biệt với ZonedTime
Thằng localdate này nó chỉ date chung chung thôi, ko có phân biệt vùng miền
Thằng zone kia thì phân biệt rõ, chỉ rõ 1 precise instant on the time line. 
Do đó thằng zone này có ưu điểm riêng là nó chính xác đến từng milimet cơ mà 1 nhược điểm to tổ bố đó 
là thằng này nó ứng với từng khu vực cục bộ, bạn set thời gian và chạy trong khu vực đó thì ko sao, sang khu vực khác, lệch múi giờ là ăn đòn liền
Birthdays, holidays, schedule times -> localDate

### Date Adjusters
### LocalTime
### LocalDateTime
ZonedDateTime apollo11launch = ZonedDateTime.of(1969, 7, 16, 9, 32, 0, 0, ZoneId.of("America/New_York")); // 1969-07-16T09:32-04:00[America/New_York]

### Formatting and parsing
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofLocalizedDateTime(FormatStyle.FULL)
dateTimeFormatter.withLocale(Locale.CHINESE);

![[Screenshot 2023-09-02 at 10.47.51.png]]


https://viblo.asia/p/co-mot-noi-so-mang-ten-timezone-Qbq5Q6MXKD8
https://viblo.asia/p/xu-ly-datetime-nhu-the-nao-cho-chuan-YWOZr3BYlQ0

![[Screenshot 2023-09-02 at 14.48.40.png]]