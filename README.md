# **Đồ án cuối kì môn Lập trình Khoa học Dữ liệu**

<div style="color: red; font-size: 20px; font-weight: bold;">Người thực hiện: Nhóm 9

- [Nguyễn Văn Quang Hưng]
- [Huỳnh Trí Nhân]
- [Chiêm Bỉnh Nguyên]
</div>

## Giới thiệu đồ án

## Môi trường sử dụng

- Ngôn ngữ Python >= 3.9
- Editor: Visual Studio Code, Jupyter Notebook
- Tổ chức file:
  - `data`: chứa dữ liệu thu thập được và dữ liệu sau khi tiền xử lý
  - `notebooks`: chứa các file mã nguồn theo từng giai đoạn của đồ án
    - 1.0-data-collecting.ipynb: file thu thập dữ liệu
    - 2.0-data-preprocessing.ipynb: file tiền xử lý dữ liệu
    - 3.0-data_explorating.ipynb: file khám phá dữ liệu
    - 4.0-questions-and-answers.ipynb: file đặt câu hỏi và trả lời
  - `images`: chứa các hình ảnh minh họa
  - `README.md`: file hướng dẫn sử dụng

## Chi tiết thực hiện

### 1. Thu thập dữ liệu

- Nguồn dữ liệu thu thập từ trang web [Kaggle](https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results)
  -Trong phần này, nhóm sử dụng chọn bộ dữ liệu Music & Mental Health Survey Results. Một bộ dữ liệu khảo sát dựa trên sở thích âm nhạc và tự đánh giá sức khỏe tinh thần của người tham gia.

  1.1. Truy cập bộ dữ liệu

- Format link: `https://www.kaggle.com/datasets/catherinerasgaitis/mxmh-survey-results`
- Nhóm tải bộ dữ liệu về và thu được một bộ dữ liệu gồm 736 mẫu với 33 cột thuộc tính.

### 2. Tiền xử lý dữ liệu

- Trong khoa học dữ liệu tiền xử lý dữ liệu quan trọng bởi vì những lý do sau:
  - Cải thiện Chất lượng Dữ liệu: Dữ liệu thô thường chứa nhiều lỗi như giá trị thiếu, không nhất quán, hoặc nhiễu. Tiền xử lý giúp làm sạch và chuẩn hóa dữ liệu, đảm bảo tính chính xác và đáng tin cậy cho phân tích.
  - Phát hiện và Xử lý Dữ liệu Ngoại lai: Dữ liệu ngoại lai có thể gây ra những hiểu lầm trong quá trình phân tích. Tiền xử lý giúp xác định và xử lý chúng một cách phù hợp.
  - Chuẩn hóa và Chuyển đổi Dữ liệu: Điều này bao gồm việc chuyển đổi dữ liệu sang các định dạng thích hợp hoặc chuẩn hóa các đặc trưng để chúng có thể được so sánh và phân tích một cách công bằng.
  - Giảm Kích thước và Tính phức tạp: Tiền xử lý có thể giúp giảm kích thước dữ liệu bằng cách loại bỏ các đặc trưng không quan trọng hoặc thông tin dư thừa, giúp quá trình học máy hiệu quả hơn.
  - Tăng cường Hiểu biết về Dữ liệu: Quá trình này cũng giúp các nhà khoa học dữ liệu hiểu rõ hơn về bản chất của dữ liệu, qua đó đưa ra những quyết định phân tích chính xác hơn.
- Các bước tiền xử lý dữ liệu là:

  - Làm sạch dữ liệu ( Data cleaning): Thường chúng ta sẽ Xử lý giá trị bị thiếu (Missing value) và loại bỏ các giá trị ngoại lai (Outlier) trong dữ liệu.
  - Chuẩn hóa và biến đổi dữ liệu (Data transformatrion): Đưa các giá trị về đúng kiểu dữ liệu, xác định biến số và biến phân loại của dữ liệu.

    2.1. Xóa những cột không cần thiết: Một số cột dữ liệu không có nhiều giá trị trong quá trình phân tích của nhóm sẽ được loại bỏ.

- Một số cột bị loại bỏ là : `'Timestamp', 'Permissions'.`

  2.2. Xử lý dữ liệu theo cột

- Chuẩn hóa dữ liệu của các cột về đúng với kiểu dữ liệu mong muốn. Vì các kiểu dữ liệu của các cột đã đúng với kiểu dữ liệu mong muốn của nhóm nên nhóm sẽ không xử lí thêm phần này.

=> Cuối cùng kiểm tra dữ liệu trùng lặp và xóa nó đi.

2.3. Xử lý dữ liệu nhiễu và thiếu

- Kiểm tra dữ liệu bị thiếu

  ![Dữ liệu bị thiếu](images/2.0-missing-values.png)

- Có các cột trên bị thiếu dữ liệu nhưng đa phần (trừ cột BPM) thì số lượng dữ liệu thiếu là không nhiều nên nhóm quyết định sẽ xóa các dòng dữ liệu bị thiếu này đi.
- Riêng cột BPM, có nhiều cách để xử lí dữ liệu thiếu nhưng trong đồ án này nhóm quyết định sẽ sử dụng thuật toán KNN để điền khuyết.

- Để có thể tiến hành áp dụng KNN thì trước tiên nhóm sẽ xử lí những dữ liệu outlier. Bởi vì các giá trị này gây ảnh hưởng tiêu cực đến kết quả. Nhóm quyết định sử dụng IQR để tìm ra các giá trị outlier của cột BPM

![Nhiễu BPM](images/2.0-BPM.png)

- Những dữ liệu outlier như 99999999.0, 624.0, 0 gây tác động rất tiêu cực đến kết quả của KNN. Vì BPM của một bài hát chỉ nằm trong khoảng 24-220 BPM. Trong trường hợp này bởi vì tiếp theo nhóm chúng em sẽ điền khuyết bằng KNN nên tạm thời chuyển những giá trị này thành np.nan và đưa vào mô hình.

![Sau KNN BPM](images/2.0-BPM-KNN.png)

=> Cuối cùng nhóm sẽ tiến hành xử lí dữ liệu nhiễu ở một số cột khác.

2.4. Xử lý dữ liệu nhiễu

- Xử lý nhiễu (noise) trong dữ liệu là một phần quan trọng của quá trình tiền xử lý trong khoa học dữ liệu. Nhiễu có thể làm giảm chất lượng dữ liệu để phân tích và đánh giá, vì vậy việc xác định và xử lý nhiễu là cần thiết.

- Những ký thuật tìm ra và xử lý nhiễu có thể là :

  - Sử dụng IQR để tìm ra các giá trị outlier của cột BPM

- Ở phần này nhóm em sẽ chủ yếu xử lí trên hai cột là `'BPM'` và `'Hours per day'`

![Outlier](images/2.0-Outlier.png)

- Sau khi xử lí outlier nhóm thu được bộ dữ liệu hoàn chỉnh với 666 mẫu và 31 cột

![Outlier2](images/2.0-Outlier2.png)

### 3. Khám phá dữ liệu

### 4. Đặt câu hỏi về bộ dữ liệu và trả lời

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
  
<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu 1:  Vấn đề về sức khỏe tinh thần của những người tham gia như thế nào ? Vấn đề này có đáng loại không?  </b></font>

<font color="red"><b>Câu hỏi có lợi ích gì: </b></font> <font color="red">Bộ dữ liệu nghiên cứu về sự tác động của âm nhạc đến với những vấn đề sức khỏe tâm lý như: Lo lắng, trầm cảm, mất ngủ và rồi loạn cưỡng chế. Do việc xem những vấn đế này có tác động đến những người tham gia là điều đáng quan tâm. Liệu những vấn đề này có tiềm tàng trong chúng ta hay không và với tỉ lệ như thế nào? Nếu lớn quá thì có đáng tâm hay không? </font>

</div>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>

<font color="red">

- Có 3 bước:

  - _Bước 1_: Xem xét sự phân bố của từng loại triệu chứng tâm lý trong từng loại bệnh.

  - _Bước 2_: Đánh giá mức độ nghiêm trọng của các triệu chứng này.

  - _Bước 3_: Vẽ biểu đồ venn thể hiện sự giao nhau của các triệu chứng

  - _Bước 4_: Đánh giá khả năng một người có thể mắc nhiều triệu chứng cùng một lúc

</font>

<font color="red"><b>Kết quả các bước làm: </b></font><font color="red">Biểu đồ Venn thể hiện mối liên hệ giữa các triệu chứng</font>

</div>

<font size="+1" color=blue><b>Bước 1: Xem xét sự phân bố của từng loại triệu chứng tâm lý trong từng loại bệnh</b></font> :
<br/><br/>

<div style="width:50%; margin:0 auto;">

<div style="width:100%;">
<caption><font size="4"><b>Điểm trung bình các triệu chứng</b></font></caption>
</div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Triệu chứng</th>
      <th>Điểm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Anxiety</td>
      <td>5.821321</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Depression</td>
      <td>4.758258</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Insomnia</td>
      <td>3.671171</td>
    </tr>
    <tr>
      <th>3</th>
      <td>OCD</td>
      <td>2.621622</td>
    </tr>
  </tbody>
</table>

</div>

![Trực quan hoá Q1](images/Q1-mental_health_spider.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Anxiety (Lo Âu): Điểm trung bình là 5.8, đây là điểm số cao nhất trong bốn loại bệnh. Điều này cho thấy tình trạng lo âu xuất hiện nhiều nhất hoặc nghiêm trọng nhất trong số các tình trạng được khảo sát. Người tham gia có xu hướng trải qua các triệu chứng lo âu ở mức độ trung bình đến khá cao.

- Depression (Trầm Cảm): Điểm trung bình là 4.75, nằm ở mức độ trung bình. Điều này chỉ ra rằng tình trạng trầm cảm cũng khá phổ biến trong nhóm người được khảo sát, nhưng không phổ biến hoặc nghiêm trọng bằng lo âu.

- Insomnia (Mất Ngủ): Điểm trung bình là 3.67, thấp hơn so với lo âu và trầm cảm. Điều này có thể cho thấy mức độ mất ngủ không quá nghiêm trọng hoặc không quá phổ biến so với hai tình trạng kia trong nhóm này.

- OCD (Rối Loạn Ám Ảnh Cưỡng Chế): Điểm trung bình thấp nhất là 2.62, cho thấy rằng trong số các tình trạng được khảo sát, OCD có vẻ ít phổ biến hoặc ít nghiêm trọng nhất.
  </b></font>

<font color="red"><b>
=> Nhìn chung, dựa trên điểm trung bình, có thể thấy rằng lo âu và trầm cảm là hai vấn đề tâm lý chính mà nhóm người tham gia khảo sát gặp phải. Điều này có thể phản ánh nhu cầu chú trọng hơn vào việc điều trị và hỗ trợ cho những người đang chịu đựng lo âu và trầm cảm.
</b></font>

</div>

<font size="+1" color=blue><b>Bước 2: Đánh giá các triệu chứng này.
</b></font>

![Trực quan hoá Q1](images/Q1-Step2.png)

<font size="+1" color=blue><b>Bước 3: Vẽ biểu đồ venn thể hiện sự giao nhau của các triệu chứng.
</b></font>

![Q1-Biểu đồ Venn](images/Q1-venn_diagram.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Từ các set ta có thể xác định được số người mắc phải triệu chứng tâm lý: khoảng 400 người mắc phải lo âu, 300 người mắc phải trầm cảm, 200 người mắc phải mất ngủ và hơn 100 người mắc phải rối loạn ám ảnh cưỡng chế.
- Sau đó là biểu đổ Venn để thể hiện mỗi liên hệ giữa các triệu chứng tâm lý. Nổi bật nhất là biểu đồ số 1 với Anxiety, Depression, Insomnia (Lo âu, Trầm cảm, Mất ngủ): Phần giao nhau lớn nhất là giữa Anxiety và Depression với 132 người, cho thấy có một số lượng lớn người tham gia mắc cả hai tình trạng này. 101 người mắc cả ba tình trạng, cũng là một con số đáng kể, chỉ ra rằng có một mối liên hệ mạnh mẽ giữa ba tình trạng này.
- Tương tự những biểu đồ còn cũng thể hiện mối liên hệ giữa các tình trạng tâm lý khác nhau. Nhưng tình trang tâm lý Anxiety và Depression nổi bật nhất, sau đó đến Insomnia và OCD chỉ có một số ít người tham gia mắc phải.
</b></font>

<font color="red"><b>
=> Tóm lại, các biểu đồ Venn này hữu ích trong việc trực quan hóa mức độ chồng chéo giữa các tình trạng tâm lý khác nhau trong một nhóm người. Chúng cho thấy rằng Anxiety và Depression có vẻ như là hai tình trạng phổ biến nhất và thường xuyên xuất hiện cùng nhau.
</b></font>

</div>

<font size="+1" color=blue><b>Bước 4: Đánh giá khả năng một người có thể mắc nhiều triệu chứng cùng lúc.
</b></font>

![Trực quan hoá Q1](images/Q1-Step2-2.png)

![Step2.2](images/Q1-percentages.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Tổng kết  </b></font>

<font color="red"><b>Sự Phổ Biến của Các Triệu Chứng:</b></font>
<font color="red">
Có một tỷ lệ đáng kể người tham gia khảo sát trải qua ít nhất một vấn đề về sức khỏe tinh thần, với một số lượng lớn người chỉ mắc một triệu chứng.
Tuy nhiên, có một số lượng không nhỏ người mắc hai triệu chứng, chỉ ra rằng sức khỏe tinh thần là một vấn đề đa diện và có thể ảnh hưởng đến người tham gia theo nhiều cách khác nhau. Có đến hơn 75% số người tham gia mắc ít nhất một triệu chứng về tình thần. Điều này phản ánh đây là vấn đề quan tâm của sức khỏe tinh thần.
</font>

<font color="red"><b>Mức Độ Nghiêm Trọng:</b></font>
<font color="red">
Dựa vào điểm trung bình của từng loại bệnh, Anxiety (Lo âu) và Depression (Trầm cảm) có điểm số cao hơn so với Insomnia (Mất ngủ) và OCD (Rối loạn ám ảnh cưỡng chế), cho thấy rằng lo âu và trầm cảm có thể là những vấn đề sức khỏe tinh thần phổ biến và nghiêm trọng hơn trong nhóm này.
</font>

<font color="red"><b>Sự Chồng Chéo Của Các triệu chứng tinh thần:</b></font>
<font color="red">
Biểu đồ Venn cho thấy có sự chồng chéo đáng kể giữa các tình trạng tâm lý. Điều này phản ánh thực tế phức tạp của sức khỏe tinh thần, nơi một người có thể trải qua nhiều vấn đề cùng một lúc, và những vấn đề này thường có mối liên quan chặt chẽ với nhau.
</font>

</div>

<br/><br/>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 2. Câu 2: Phân tích những lựa chọn, sở thích nghe nhạc của những người tham gia khảo sát khi các triệu chứng tinh thần diễn ra thường xuyên hơn (> 5 ở thang 10) có gì thay đổi hay không?
</b></font>

<font color="red"><b>Câu hỏi có lợi ích gì: </b></font> <font color="red">Việc phân tích những yếu tố tác động đến sức khỏe tinh thân giúp chúng ta có cái nhìn chi tiết hơn về vấn để tinh thần của mọi người. Nhìn nhận việc nghe nhạc tác động đến sức khỏe ở nhiều góc cạnh khác nhau, tìm ra những khác biệt của những người các triệu chứng về sức khỏe tinh thần, để kip thời phát hiện và chữa trị sớm nhất</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 3 bước:

  - _Bước 1_: Đánh giá số giờ nghe nhạc của những người có mức độ của các triệu chứng cao so với những người còn lại.

  - _Bước 2_: Đánh giá tần suất nghe nhạc của những người có mức độ của các triệu chứng cao so với những người còn lại.

  - _Bước 3_: Đánh giá về sở thích âm nhạc của nhóm người này.

  - _Bước 4_: Đánh giá mức độ ảnh hưởng của âm nhạc lên sức khỏe tinh thần của họ.

    </font>

</div>

<font size="+1" color=blue><b>Bước 1: Đánh giá số giờ nghe nhạc của những người có mức độ của các triệu chứng cao so với những người còn lại.
</b></font>

![Số giờ](images/Q2-diferrence-average_hours.png)

<font size="+0.5"> <b>

- Có thể thấy trung bình số giờ nghe nhạc trong ngày của các nhóm người này cao hơn so với trung bình của tất cả mọi người nhưng không đáng kể
- Tiếp theo chúng ta tìm hiểu tần suất nghe nhạc của những người này ở từng thể loại nhạc
  </b>
  </font>

<font size="+1" color=blue><b>Bước 2: Đánh giá tần suất nghe nhạc của những người có mức độ của các triệu chứng cao so với những người còn lại.
</b></font>

![All](images/Q2-percentages-all.png)
![Anxiety](images/Q2-percentages-anxiety.png)
![Depression](images/Q2-percentages-depression.png)
![Insomnia](images/Q2-percentages-insomnia.png)
![OCD](images/Q2-percentages-ocd.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Tần suất trung bình  tất cả mọi người so với Người Có Lo Âu: Trong biểu đồ dành cho những người có triệu chứng lo âu, có thể thấy rõ ràng tần suất nghe hầu hết các thể loại nhạc đều tăng lên, đặc biệt là Rock và Pop, cho thấy những người lo âu có thể sử dụng việc nghe nhạc như một phương pháp tự giúp bản thân nhiều hơn người bình thường.

- Tần suất trung bình tất cả mọi người so với Người Có Trầm Cảm: Những người có trầm cảm cho thấy tần suất nghe nhạc Metal và Rock cao đáng kể. Điều này có thể ám chỉ một sở thích đối với các thể loại có thể phản ánh hoặc ảnh hưởng đến tình trạng cảm xúc của họ.

- Tần suất trung bình tất cả mọi người với Người Có Mất Ngủ: Những người mất ngủ nghe nhạc video game và Metal với tần suất cao hơn. Điều này có thể chỉ ra rằng họ sử dụng nhạc như một phương tiện để gây ngủ hoặc quản lý căng thẳng liên quan đến tình trạng mất ngủ.

- Tần suất trung bình tất cả mọi người so với Người Có OCD (Rối Loạn Ám Ảnh Cưỡng Chế): Tần suất nghe nhạc Rap và Pop cao hơn đáng kể ở những người có OCD. Có thể nhịp điệu và tính dự đoán trong các thể loại này h resonates hơn với những người nghe có OCD.

- Xuyên suốt tất cả các biểu đồ, nhạc Gospel thường có tần suất nghe thấp hơn ở những người có các điều kiện này so với dân số tổng thể, có thể cho thấy rằng thể loại này ít được sử dụng hoặc ít hiệu quả như một chiến lược đối phó cho những nhóm cụ thể này.
  </b></font>

<font color="red"><b>
=> Các biểu đồ cho thấy những người có vấn đề sức khỏe tâm thần có thể có thói quen nghe nhạc khác biệt so với dân số chung, có khả năng sử dụng nhạc nhiều hơn như một công cụ trị liệu hoặc như một phản ánh của tình trạng cảm xúc của họ
</b></font>

</div>

<font size="+1" color=blue><b>Bước 3: Đánh giá về sở thích âm nhạc của nhóm người này.
</b></font>

![Gerne](images/Q2-genre_counts.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Thể loại Rock dường như là thể loại được yêu thích nhất trong số các nhóm có các triệu chứng tâm thần, với số lượng người yêu thích đáng kể trong mỗi nhóm.
- Pop và Metal cũng là những thể loại được nhiều người yêu thích, đặc biệt là trong nhóm người có triệu chứng lo âu và trầm cảm.
- Nhạc cổ điển và nhạc video game có số lượng người yêu thích tương đối ổn định giữa các nhóm, nhưng không phải là thể loại được yêu thích nhất.
- Những thể loại như Hip hop, Folk, EDM, R&B, K-pop, và Jazz có số lượng người yêu thích ít hơn so với Rock, Pop, và Metal.
- Thể loại Country, Lofi, Rap, Gospel, và Latin có số lượng người yêu thích ít nhất trong các nhóm này.
</b></font>
</div>

<font size="+1" color=blue><b>Bước 4: Đánh giá mức độ ảnh hưởng của âm nhạc lên sức khỏe tinh thần của họ.
</b></font>

![Effect](images/Q2-music_effects.png)

<font size="+1" color=#215C67><b>
Nhìn chung, những biểu đồ này cho thấy rằng đa số mọi người, bao gồm cả những người có triệu chứng bệnh cụ thể, đều cảm thấy có lợi khi nghe nhạc. Tuy nhiên, tỷ lệ những người cảm thấy xấu đi khi nghe nhạc tăng lên đôi chút trong các nhóm có các triệu chứng bệnh, điều này có thể phản ánh sự cần thiết của việc lựa chọn đúng loại nhạc cho từng cá nhân và tình trạng sức khỏe tâm thần cụ thể của họ.
</b></font>

</font>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Tổng kết nghiên cứu  </b></font>

<font color="red"><b>Câu hỏi: </b></font>
<font color="red">Phân tích so sánh sự ảnh hưởng của âm nhạc đối với cảm xúc và tình trạng tâm thần của mọi người, cũng như những người đang trải qua các triệu chứng tâm thần như lo âu, trầm cảm, mất ngủ và OCD.</font>

<font color="red"><b>Trả lời :</b></font>
<font color="red">

Từ biểu đồ tần suất nghe nhạc, chúng đã phát hiện ra rằng:

- Người có triệu chứng lo âu và trầm cảm có xu hướng nghe nhạc Rock và Pop nhiều hơn.
- Người mất ngủ có xu hướng nghe nhạc video game và Metal nhiều hơn.
- Người có OCD nghe nhạc Rap và Pop nhiều hơn so với mức trung bình.

Từ biểu đồ sở thich âm nhạc của những người có triệu chứng bệnh ta thấy: ở thích âm nhạc cá nhân có liên quan đến triệu chứng tâm thần và có thể phản ánh cách thức mà mỗi người đối phó với tình trạng sức khỏe tâm thần của họ. Thể loại Rock và Pop được yêu thích rộng rãi trong tất cả các nhóm, trong khi các thể loại khác như Metal có thể được ưa chuộng bởi những người trải qua trạng thái cảm xúc sâu sắc hơn. Sự đa dạng trong sở thích âm nhạc cho thấy việc lựa chọn âm nhạc để hỗ trợ sức khỏe tâm thần là một trải nghiệm rất cá nhân và cần phải được cá nhân hóa.

Biểu đồ về ảnh hưởng của âm nhạc cho thấy:

- Đa số mọi người trong các nhóm triệu chứng khác nhau đều cảm thấy cải thiện khi nghe nhạc, với tỷ lệ cao nhất là ở những người có lo âu.
- Có một tỷ lệ nhỏ người cảm thấy tình trạng của họ xấu đi khi nghe nhạc, đặc biệt là ở nhóm người mất ngủ.
- Số lượng người không cảm thấy có tác động gì từ âm nhạc cũng khá đáng kể.

=> hững phát hiện này cho thấy âm nhạc có thể đóng vai trò là một công cụ hữu ích trong việc cải thiện tình trạng tâm thần hoặc ít nhất là cung cấp một phương tiện thoải mái và giải trí cho người nghe. Tuy nhiên, cũng có một tỷ lệ nhất định mà âm nhạc không mang lại hiệu quả tích cực hoặc thậm chí có thể làm tình hình tồi tệ hơn, điều này nhấn mạnh tầm quan trọng của việc lựa chọn đúng loại nhạc cho từng cá nhân.

Qua đó, nghiên cứu của bạn đã cung cấp cái nhìn sâu sắc về mối liên hệ giữa âm nhạc và sức khỏe tâm thần, đồng thời cũng phản ánh sự khác biệt về sở thích âm nhạc giữa những người có triệu chứng tâm thần so với dân số chung. Những thông tin này có thể hữu ích cho việc phát triển các chương trình can thiệp sức khỏe tâm thần thông qua âm nhạc hoặc chỉ đơn giản là cung cấp kiến thức cho những người đang tìm cách sử dụng âm nhạc để cải thiện tâm trạng của mình.

</font>

</div>

<br/><br/>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu 3: Những người ở độ tuổi khác nhau có sở thích về âm nhạc khác nhau như thế nào? Xu hướng thưởng thức âm nhạc của họ ảnh hưởng như thế nào?
</b></font>

<font color="red"><b>Câu hỏi có lợi ích gì: </b></font> <font color="red">Việc phân tích những yếu tố tác động đến sức khỏe tinh thân giúp chúng ta có cái nhìn chi tiết hơn về vấn để tinh thần của mọi người. Nhìn nhận việc nghe nhạc tác động đến sức khỏe ở nhiều góc cạnh khác nhau, tìm ra những khác biệt của những người các triệu chứng về sức khỏe tinh thần, để kip thời phát hiện và chữa trị sớm nhất</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 3 bước:

  - _Bước 1_: Thống kê độ tuổi của mọi người theo thể loại nhạc yêu thích

  - _Bước 2_: Chia các nhóm tuổi và tiến hành đánh giá lại

  - _Bước 3_: Đánh giá mức độ nghiêm trọng của các triệu chứng tâm lý theo nhóm tuổi

</font>

</div>

<font size="+1" color=blue><b>Bước 1: Thống kê độ tuổi của mọi người theo thể loại nhạc yêu thích
</b></font>

![Alt text](images/Q3-age_fav_genre.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
Các thể loại như Video game music và Jazz có sự phân bố độ tuổi rộng, chỉ ra rằng chúng được nghe bởi một lượng người nghe đa dạng về tuổi tác.
Rock và Pop có nhiều điểm ngoại lệ, cho thấy có người nghe ở độ tuổi cao hơn so với phần lớn người nghe thể loại này.
Thể loại như Classical và Metal có sự phân bố tuổi tương đối hẹp, chỉ ra rằng đối tượng nghe nhạc có xu hướng tập trung vào một nhóm tuổi nhất định.
Lofi và Gospel có những người nghe ở độ tuổi thấp, dựa vào vị trí của hộp và độ rộng của nó.
Latin music dường như có số lượng người nghe ít nhất và có phân bố tuổi hạn chế so với các thể loại khác.
</b></font>
</div>

- Có vẻ như số lượng người tham gia không khảo sát được toàn bộ các độ tuổi. Khó có thể đánh giá theo từng độ tuổi được. Để tiếp tục đánh giá được, chúng ta sẽ chia ra thành các nhóm tuổi
- Vì độ tuổi phân bố khác nhau trong bộ dữ liệu. Nên chúng em quyết định chia độ tổi thành các khoảng dựa theo quantitle của dữ liệu. Chúng em lựa chọn bins là 10 để đánh giá.

<font size="+1" color=blue><b>Bước 2: Chia các nhóm tuổi và tiến hành đánh giá lại
</b></font>

- Sau khi chia nhóm tuổi ta có tỉ lệ các nhóm như sau:
  ![Alt text](images/Q3-age_percentage.png)

- Tiến hành đánh giá lại sở thích âm nhạc theo từng nhóm tuổi

![Alt text](images/Q3-age_fav_genre_stacked.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Phân bố độ tuổi: Có vẻ như mỗi nhóm tuổi có sự yêu thích khác nhau đối với các thể loại nhạc. Thể loại nhạc "Rock" và "Pop" dường như phổ biến trong hầu hết các nhóm tuổi, với số lượng người yêu thích đáng kể. Nhưng thể loại "Rock" thì những người trên 30 tuổi có vẻ như nghe nhiều hơn.

- Thể loại nhạc phổ biến: Thể loại "Video game music" nổi bật trong nhóm tuổi trẻ, trong khi "Classical" được yêu thích bởi nhóm tuổi "Trên 40 tuổi" và nhóm tuổi "Dưới 16"

- Sự đa dạng trong sở thích: Mỗi nhóm tuổi có sự đa dạng trong sở thích âm nhạc của họ, không có thể loại nhạc nào chiếm ưu thế tuyệt đối trong bất kỳ nhóm tuổi nào.

- Ngoại lệ và biến động: Có một số ngoại lệ trong từng nhóm tuổi, như thể hiện qua số lượng người yêu thích nhất định trong các thể loại nhạc khác nhau. Điều này cho thấy sự đa dạng trong sở thích cá nhân không hoàn toàn bị hạn chế bởi độ tuổi.
  </b></font>

<font color="red"><b>
=> Tóm lại, biểu đồ cung cấp cái nhìn tổng quan về sự phân bố sở thích âm nhạc qua các nhóm tuổi và cho thấy âm nhạc là một phần của văn hóa đa dạng, với mỗi nhóm tuổi đều có những sở thích riêng biệt và độc đáo của họ.
</b></font>

</div>

Vậy xu hướng thưởng thức âm nhạc của mỗi người có sự khác biệt dựa trên tuổi tác của họ không?

- Chúng ta hãy xem mọi người có nghe nhạc lúc làm việc, chơi nhạc cụ để thưởng thức âm nhạc hay có thói quen sáng tác nhạc như một cách hưởng thụ âm nhạc hay không, và cuối cùng có thích thể loại nước ngoài hay không?
- Ở phần chỉ có 2 xu hướng là có hoặc không nên chúng ta sẽ xem xét sự phân bố của những người tham gia theo độ tuổi.

![Alt text](images/Q3-age_binary_heatmap.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Tỉ lệ những người đang làm việc ("While working") khá cao qua tất cả các nhóm tuổi, đặc biệt là nhóm "16 tuổi trở xuống" và "18-19 tuổi" với tỉ lệ cao nhất.
- Nhóm "16-17 tuổi" và "17-18 tuổi" có tỉ lệ cao những người chơi nhạc cụ ("Instrumentalist") và sáng tác nhạc ("Composer"), nhưng tỉ lệ này giảm dần ở các nhóm tuổi lớn hơn.
- Hoạt động khám phá các nghệ sĩ thể loại nhạc  ("Exploratory") sau khi nghe có tỉ lệ thấp nhất ở nhóm "Trên 40 tuổi", cho thấy sự giảm nhu cầu hoặc sự quan tâm đến hoạt động khám phá ở nhóm tuổi này.
- nghe nhạc nước ngoài ("Foreign languages") được quan tâm nhiều ở nhóm tuổi trẻ, đặc biệt là nhóm "16-17 tuổi" với tỉ lệ cao nhất, và tỉ lệ này giảm dần khi tuổi tác tăng lên.
</b></font>
</div>

<font size="+1" color=blue><b>Bước 3: Đánh giá mức độ nghiêm trọng của các triệu chứng tâm lý theo nhóm tuổi
</b></font>

![Alt text](images/Q3-age_mental_health.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Nhìn vào biểu đồ cho thấy rằng tổng số lượng triệu chứng tâm lý theo từng nhóm tuổi cùng với đó là số lượng từng loại bệnh. 
- Biểu đồ nhìn chung, giai đoạn tuổi từ 16 đến 21 tuổi, khi tâm lý chưa vững vàng, con người có thể xuất hiện nhiều triệu chứng tâm lý nhất và biến động không thể kiểm soát đươc. 
- Số lượng người bị các vấn đề về Lo lắng, Mất ngủ và OCD lại xuất hiện nhiều nhất ở những bạn dưới 16 tuổi (điều này có vẻ không hợp lý) 
- ở độ tuổi từ 19-23 tuổi, dường như các vấn đề xuất hiện nhiều nhất là Trầm cảm và Lo lắng. Đây là điều dễ hiểu vì đây là giai đoạn mà con người bắt đầu có những áp lực lớn về học tập, công việc, tương lai, tình cảm,..
- Dần về sau thì những người bị các triệu chứng thì ít hơn theo độ tuổi. Điều này có thể hiểu là khi con người trưởng thành, có thể tự kiểm soát được tâm lý của mình hơn.

</b></font>

<font color="red"><b>
=> tổng số lượng người có vấn để tâm lý cũng xuất hiện nhiều nhất ở những người 16 tuổi trở xuống, sau đó là độ tuổi từ 19-23. Điều này cho thấy rằng các bệnh đang dần trẻ hóa đi, và đặt ra mối quan tâm đến tâm lý ở những bạn trẻ nhiều hơn.
Nếu không điều trị sớm có thể dẫn đến những hậu quả khó lường
</b></font>

</div>

<br></br>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 4. Số nhịp điệu của dòng dòng nhạc yêu thích có ảnh hưởng tới sức khỏe tinh thần của họ hay không?
</b></font>

<font color="red"><b>Câu hỏi có lợi ích gì: </b></font> <font color="red"></font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 4 bước:

  - _Bước 1_: Vẽ histogram các mức BPM, thống kê BPM trung bình của các dòng nhạc

  - _Bước 2_: Phân các dòng nhạc thành các nhóm theo mức BPM

  - _Bước 3_: Đánh giá mức độ ảnh hưởng của BPM đến các triệu chứng tâm lý

</font>

</div>

<font size="+1" color=blue><b>Bước 1: Vẽ histogram các mức BPM, thống kê BPM trung bình của các dòng nhạc
</b></font>

![Alt text](images/Q4-BPM-histogram.png)

- Thống kê mức BPM trung bình cho các dòng nhạc

![Alt text](images/Q4-BPM-Favgen-boxplot.png)

<font size="+1" color=blue><b>Bước 2: Phân các dòng nhạc thành các nhóm theo mức BPM
</b></font>

![Alt text](images/Q4-Describe.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>

Dựa vào biểu đồ và những dữ liệu chi tiết có thể thấy rõ sự phân chia nhịp độ trung bình (BPM) giữa các thể loại nhạc:

- Nhóm Nhịp Độ Cao: Metal và EDM đứng đầu danh sách với BPM trung bình cao nhất, cho thấy đây là các thể loại nhạc có năng lượng và độ sôi động rất cao.

- Nhóm Nhịp Độ Trung Bình đến Cao: Rap, K pop, Rock, và Video game music có BPM trung bình từ khoảng 120 đến 126, cho thấy những thể loại này thường có nhịp điệu nhanh và phù hợp với nhu cầu giải trí đa dạng.

- Nhóm Nhịp Độ Trung Bình đến Thấp: Gospel, Pop, Classical, R&B, Jazz, Folk và Hip hop có BPM trung bình nằm trong khoảng từ khoảng 115 đến 120. Các thể loại này có thể bao gồm cả bản nhạc nhanh và chậm, phản ánh sự đa dạng trong cách biểu đạt và cảm xúc trong âm nhạc.

- Nhóm Nhịp Độ Thấp:Lofi và Country có BPM trung bình dưới 115 BPM, thấp hơn các thể loại kể trên, điều này phản ánh tính chất nhẹ nhàng và tình cảm của thể loại nhạc này.

- Đáng chú ý: Latin chỉ có một bài hát được đưa vào dữ liệu với BPM là 73, có thể không đại diện cho toàn bộ thể loại nhạc Latin.
  </b></font>

<font color="red"><b>
=> Nói chung, BPM trung bình phản ánh không chỉ phong cách và đặc trưng của các thể loại nhạc mà còn cho thấy sở thích và xu hướng của người nghe nhạc. Thể loại nhạc có BPM cao thường liên quan đến năng lượng và sự hứng khởi, trong khi thể loại nhạc có BPM thấp hơn mang lại không gian tĩnh lặng và sâu lắng hơn.
</b></font>

</div>

<font size="+1" color=blue><b>Bước 3: Đánh giá mức độ ảnh hưởng của BPM đến các triệu chứng tâm lý
</b></font>

![Alt text](images/Q4-scatter3D-mental_health_bpm_genre.png)

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>
- Ở các người tham gia có xu hướng Lo lắng và Trầm Cảm cao dể dàng nhận thấy rằng họ thường nghe những loại nhạc Rock, Rap, Metal,Pop,  R&B, Rap, Rock. Ở mức BPm trên 120 thì họ sẽ có nhiều triệu chứng hơn. Nhưng trái ngược lại họ ít có cảm giác đốt với các triệu chứng Mất ngủ hay OCD.

- Riêng thể loại nhạc EDM tuy có xung nhịp cao nhưng rất ít người yêu thích thể loại nhạc đó cảm thấy có vấn đề đối với trạng thái tinh thần của mình so với những thể loại nhạc có cùng xung nhịp khác.
  </b></font>

<font color="red"><b>
=> Thể loại nhạc và xung nhịp của loại nhạc đó cũng có một tác động lớn đến các vấn đề tâm lý. Nhìn vào biểu đồ có thể thấy những loại nhạc có mức độ xung nhịp trên 120 có thể ảnh hưởng đến tinh thần của mọi người, khiên cho mọi người cảm thấy bất an, lo âu và có xu hướng xuất hiện cái triệu chứng tinh thần thường xuyên hơn.
</b></font>

</div>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 5. Mức độ ảnh hưởng của các thuộc tính dữ liệu đến với các vấn đề tâm lý ở mức độ như thế nào?
</b></font>

<font color="red"><b>Câu hỏi có lợi ích gì: </b></font> <font color="red">Qua các câu hỏi trên, phần nào đã định hình được mức độ ảnh hưởng của âm nhạc lên sức khỏe tinh thần của chúng ta. Nhưng để hiểu chính xác mức độ ảnh hưởng lớn như thế nào ta cần phải minh họa trực quan bằng những con số, cái mà những mô hình dựa vào đó để dự đoán cột mục tiêu</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 4 bước:

  - _Bước 1_: Xử lí dữ liệu đầu vào

  - _Bước 2_: Trích xuất các cột số và cột phân loại để đánh giá

  - _Bước 3_: Tiến hành đánh giá

</font>

</div>

<font size="+1" color=blue><b>Bước 1: Xử lí dữ liệu đầu vào
</b></font>

- Tiến hành đưa các cột dữ liệu đánh giá mức độ các triệu chứng về kiểu int, cột nhóm tuổi về kiểu object.

- Loại bỏ các cột không cần thiết: `'Age', 'Fav gerne encoded'`

- Chuẩn hóa lại tên các cột.

<font size="+1" color=blue><b>Bước 2: Trích xuất các cột số và cột phân loại để đánh giá
</b></font>

![Q5-Trích xuất](images/Q5-Trich-xuat.png)

<font size="+1" color=blue><b>Bước 3: Tiến hành đánh giá
</b></font>

- Sau khi đánh giá bằng cách phương pháp Anova, Pearson lần lượt cho các cột phân loại và cột số, nhóm thu được kết quả như sau:

  - Anova

  ![Anova](images/Q5-Anova.png)

  - Pearson

  ![Pearson](images/Q5-Pearson.png)

## Tác giả

- [Nhóm 9] (https://github.com/HungLVT/DS.git)

## Liên hệ

- [Nguyễn Văn Quang Hưng]
- [Huỳnh Trí Nhân]
- [Chiêm Bỉnh Nguyên]
