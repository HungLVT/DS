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

<font size="+0.5"> <b>

- Các giá trị được lọc ra trong `Yêu cầu bằng cấp` là `Chứng chỉ`,`Trên đại học`

- Các giá trị được lọc ra trong `Yêu cầu kinh nghiệm` là `Hơn 4 năm`,`4 năm`
  </b>
  </font>

<font size="+1" color=blue><b>Bước 2: Lọc các giá ngoại lại trong cột 'Mức lương trung bình'
</b></font>

<div>

<table border="1" class="dataframe">
<caption><font size="4"><b> Bảng dữ liệu sau khi lọc các giá trị ngoại lai</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Khu vực tuyển</th>
      <th>Thời gian thử việc</th>
      <th>Cấp bậc</th>
      <th>Yêu cầu giới tính</th>
      <th>Số lượng tuyển</th>
      <th>Hình thức làm việc</th>
      <th>Yêu cầu bằng cấp</th>
      <th>Yêu cầu kinh nghiệm</th>
      <th>Ngành nghề</th>
      <th>Quy mô công ty</th>
      <th>Loại công ty</th>
      <th>Mức lương thấp nhất</th>
      <th>Mức lương cao nhất</th>
      <th>Mức lương trung bình</th>
      <th>Tuổi thấp nhất</th>
      <th>Tuổi cao nhất</th>
      <th>Tuổi trung bình</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>560</th>
      <td>TP.HCM</td>
      <td>1.8</td>
      <td>Cộng tác viên</td>
      <td>Không yêu cầu</td>
      <td>5</td>
      <td>Bán thời gian cố định</td>
      <td>Không</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Kế toán/Thực tập sinh/Hành chính - Thư ký</td>
      <td>Trên 300 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>1.0</td>
      <td>3.0</td>
      <td>2.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>315</th>
      <td>Long An</td>
      <td>2.0</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>1</td>
      <td>Toàn thời gian cố định</td>
      <td>Trung cấp</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Hành chính - Thư ký/Biên phiên dịch</td>
      <td>Trên 300 người</td>
      <td>Công ty cổ phần</td>
      <td>14.0</td>
      <td>25.0</td>
      <td>19.5</td>
      <td>22.0</td>
      <td>35.0</td>
      <td>28.5</td>
    </tr>
    <tr>
      <th>524</th>
      <td>TP.HCM</td>
      <td>1.8</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>2</td>
      <td>Toàn thời gian cố định</td>
      <td>Trung cấp</td>
      <td>1 năm</td>
      <td>Kế toán/Thu mua - Kho Vận - Chuỗi cung ứng/Hàn...</td>
      <td>10 - 150 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>8.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>23.0</td>
      <td>35.0</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>3538</th>
      <td>TP.HCM</td>
      <td>1.6</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>2</td>
      <td>Toàn thời gian cố định</td>
      <td>Cao đẳng</td>
      <td>3 năm</td>
      <td>Kế toán/Kiểm toán/Tài chính - Đầu tư - Chứng K...</td>
      <td>10 - 150 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>9.0</td>
      <td>10.0</td>
      <td>9.5</td>
      <td>23.0</td>
      <td>40.0</td>
      <td>31.5</td>
    </tr>
    <tr>
      <th>2849</th>
      <td>Gia Lai</td>
      <td>2.0</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>1</td>
      <td>Toàn thời gian cố định</td>
      <td>Trung học</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Bán hàng - Kinh doanh/Tài chính - Đầu tư - Chứ...</td>
      <td>Trên 300 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>15.0</td>
      <td>25.0</td>
      <td>20.0</td>
      <td>25.0</td>
      <td>40.0</td>
      <td>32.5</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 3: Trực quan hoá
</b></font>

![Trực quan hoá Q2](images/3.0-question2.1.png)

![Trực quan hoá Q2](images/3.0-question2.2.png)

<font size="+1.5" color="blue"><b>=>Trả lời câu hỏi
</b></font>

<font>

- Ở biểu đồ về <b>Kinh nghiệm</b>, dễ dàng nhận thấy với kinh nghiệm càng cao thì mức lương nhận được càng cao
- Ở biểu đồ về <b>Bằng cấp</b>, với bằng đại học thì mức lương được trỉa rộng nhất và cao nhất, các bằng cấp còn lại không khác biệt nhiều

</font>

<br/><br/>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 3. Khác biệt trong nhu cầu tuyển dụng ở các tỉnh thành khác nhau ?
</b></font>

<font color="red"><b>Mục đích của câu hỏi: </b></font> <font color="red">Cho người tìm việc làm hiểu được nhu cầu của thị trường ở các địa phương cụ thể</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 3 bước:

  - _Bước 1_: Lần lượt tách tất cả các hàng dữ liệu khi tại hàng đó và cột cụ thể có chứa hơn 1 giá trị, ví dụ ở cột `Khu vực tuyển` có các hàng có giá trị là nhiều hơn 1 tỉnh, để làm việc này, nhóm sẽ tách các giá trị ở các hàng trong một cột theo giá trị ngăn cách như `/` hoặc `, `. Sau đó sẽ explode theo cột.

  - _Bước 2_: Gom nhóm theo các cột dữ liệu `Khu vực tuyển`, `Ngành nghề`,và tính tổng ở cột `Số lượng tuyển` sau đó so sánh số lượng tuyển các ngành ở các tỉnh thành cụ thể. Ở đây nhóm sẽ xem xét ở 5 khu vực tuyển có số lượng tuyển nhiều nhất

  - _Bước 3_: Vẽ 5 biểu đồ cột để so sánh, vì có rất nhiều ngành nghề nên nhóm chỉ trực quan ở 5 ngành nghề có số lượng tuyển cao nhất<font color="red"></font>

</font>

<font color="red"><b>Kết quả các bước làm: </b></font><font color="red">5 biểu đồ cột đôi so sánh số lượng tuyển của các ngành nghề</font>

</div>

<font size="+1" color=blue><b>Bước 1: Tách các cột dữ liệu
</b></font>

<font size="+0.5"> <b>
Tách các cột dữ liệu `Ngành nghề` và `Khu vực tuyển` thành các giá trị riêng biệt
</b>
</font>

<div>

<table border="1" class="dataframe">
<caption><font size="4"><b>Bảng dữ liệu sau khi tách</b></font></caption>

  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Khu vực tuyển</th>
      <th>Thời gian thử việc</th>
      <th>Cấp bậc</th>
      <th>Yêu cầu giới tính</th>
      <th>Số lượng tuyển</th>
      <th>Hình thức làm việc</th>
      <th>Yêu cầu bằng cấp</th>
      <th>Yêu cầu kinh nghiệm</th>
      <th>Ngành nghề</th>
      <th>Quy mô công ty</th>
      <th>Loại công ty</th>
      <th>Mức lương thấp nhất</th>
      <th>Mức lương cao nhất</th>
      <th>Mức lương trung bình</th>
      <th>Tuổi thấp nhất</th>
      <th>Tuổi cao nhất</th>
      <th>Tuổi trung bình</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>7072</th>
      <td>Bắc Ninh</td>
      <td>1.8</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Nam</td>
      <td>10</td>
      <td>Toàn thời gian cố định</td>
      <td>Trung cấp</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Khoa học - Kỹ thuật</td>
      <td>Trên 300 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>8.0</td>
      <td>10.0</td>
      <td>9.0</td>
      <td>25.0</td>
      <td>36.0</td>
      <td>30.5</td>
    </tr>
    <tr>
      <th>15092</th>
      <td>Hải Phòng</td>
      <td>0.5</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Nữ</td>
      <td>1</td>
      <td>Toàn thời gian cố định</td>
      <td>Đại học</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Công nghệ thực phẩm - Dinh dưỡng</td>
      <td>150 - 300 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>8.0</td>
      <td>12.0</td>
      <td>10.0</td>
      <td>21.0</td>
      <td>45.0</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>8895</th>
      <td>TP.HCM</td>
      <td>2.0</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>10</td>
      <td>Toàn thời gian cố định</td>
      <td>Cao đẳng</td>
      <td>Dưới 1 năm</td>
      <td>Ngân hàng</td>
      <td>Trên 300 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>8.0</td>
      <td>20.0</td>
      <td>14.0</td>
      <td>22.0</td>
      <td>35.0</td>
      <td>28.5</td>
    </tr>
    <tr>
      <th>6156</th>
      <td>TP.HCM</td>
      <td>2.0</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>1</td>
      <td>Toàn thời gian cố định</td>
      <td>Đại học</td>
      <td>2 năm</td>
      <td>IT Phần mềm</td>
      <td>Dưới 10 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>12.0</td>
      <td>25.0</td>
      <td>18.5</td>
      <td>25.0</td>
      <td>45.0</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>4312</th>
      <td>TP.HCM</td>
      <td>1.6</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Không yêu cầu</td>
      <td>10</td>
      <td>Toàn thời gian cố định</td>
      <td>Cao đẳng</td>
      <td>1 năm</td>
      <td>Bán sỉ - Bán lẻ - Quản lý cửa hàng</td>
      <td>10 - 150 người</td>
      <td>Công ty trách nhiệm hữu hạn</td>
      <td>15.0</td>
      <td>20.0</td>
      <td>17.5</td>
      <td>23.0</td>
      <td>34.0</td>
      <td>28.5</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 2: Gom nhóm dữ liệu theo `Khu vực tuyển` và `Ngành nghề`, lấy tổng ở cột ` Số lượng tuyển`
</b></font>

<div>

<table border="1" class="dataframe">
  <caption><font size="4"><b>Bảng dữ liệu số lượng tuyển theo tưng ngành nghề và khu vực tuyển</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Khu vực tuyển</th>
      <th>Ngành nghề</th>
      <th>Số lượng tuyển</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1309</th>
      <td>Vĩnh Phúc</td>
      <td>Ngân hàng</td>
      <td>116</td>
    </tr>
    <tr>
      <th>1256</th>
      <td>Tây Ninh</td>
      <td>Quản lý dự án</td>
      <td>5</td>
    </tr>
    <tr>
      <th>272</th>
      <td>Bắc Ninh</td>
      <td>Xuất Nhập Khẩu</td>
      <td>9</td>
    </tr>
    <tr>
      <th>532</th>
      <td>Hải Dương</td>
      <td>Bảo hiểm</td>
      <td>15</td>
    </tr>
    <tr>
      <th>1214</th>
      <td>Trà Vinh</td>
      <td>Ngân hàng</td>
      <td>33</td>
    </tr>
    <tr>
      <th>883</th>
      <td>Phú Thọ</td>
      <td>Xây dựng</td>
      <td>2</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Bình Phước</td>
      <td>An ninh - Bảo vệ</td>
      <td>2</td>
    </tr>
    <tr>
      <th>1448</th>
      <td>Đồng Nai</td>
      <td>Khoa học - Kỹ thuật</td>
      <td>65</td>
    </tr>
    <tr>
      <th>846</th>
      <td>Ninh Bình</td>
      <td>Kế toán</td>
      <td>6</td>
    </tr>
    <tr>
      <th>36</th>
      <td>Bà Rịa - Vũng Tàu</td>
      <td>Dược phẩm</td>
      <td>77</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 3: Trực quan hoá
</b></font>

![Trực quan hoá Q3.1](images/3.0-question3.1.png)

![Trực quan hoá Q3.2](images/3.0-question3.2.png)

![Trực quan hoá Q3.3](images/3.0-question3.3.png)

![Trực quan hoá Q3.4](images/3.0-question3.4.png)

![Trực quan hoá Q3.4](images/3.0-question3.4.png)

<font size="+1.5" color="blue"><b>=>Trả lời câu hỏi
</b></font>

<font>

- Biểu đồ cho thấy giống như biểu đồ về tuyển dụng các ngành ở phần khám phá, ngành <b>Bán hàng - kinh doanh, Hành chính - Thư ký, Chăm sóc khách hàng </b> luôn có số lượng tuyển cao ở các tỉnh.

- Ngành <b>Khách sạn - Nhà hàng - Du lịch </b> xuất hiện ở 4/5 biểu đồ dù không phải nằm trong top 10 ngành có số lượng tuyển nhiều nhất cả nước

- Tại tỉnh <b>Long An</b>, <b> Nghề nghiệp khác</b> chiếm số lượng tuyển khá lớn - Đứng thứ 2 trong toàn bộ số lượng tuyển

- Các ngành nghề <b>Lao động phổ thông, Chăm sóc khách hàng</b> cũng có xuất hiện dù không nằm trong top 10 toàn quốc

</font>

<br></br>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 4. Với độ tuổi cụ thể, người lao động có thể tìm đến những việc làm nào và tiền lương có thể nhận được là bao nhiêu ?
</b></font>

<font color="red"><b>Mục đích của câu hỏi: </b></font> <font color="red">Giúp người lao động có thể tìm việc phù hợp với độ tuổi và lương mong muốn</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 4 bước:

  - _Bước 1_: Xem xét biểu đố histogram của cột tuổi, tiến hành chia lại thành các nhóm tuổi `16-25`, `26-30`, `31-60` và lưu vào cột mới là `Nhóm tuổi`

  - _Bước 2_: Tách các hàng mang nhiều giá trị trong cột `Ngành nghề`, dùng explode để tách

  - _Bước 3_: Tạo bảng để tính số lượng cho mỗi `Ngành nghề` và `Nhóm tuổi`

  - _Bước 4_: Vẽ biểu đồ cột nhiều màu để so sánh, đồng thời biểu diễn lương trung bình bên cạnh mỗi màu trong cột

</font>

<font color="red"><b>Kết quả các bước làm: </b></font><font color="red">Biểu đồ cột đôi so sánh mức lương của nam và nữ trong cùng một điều kiện ở 5 ngành nghề có số lượng tuyển nhiều nhất</font>

</div>

<font size="+1" color=blue><b>Bước 1: Xem xét histogram độ tuổi và chia lại các bins
</b></font>

![Histogram Q4](images/3.0-question4.1.png)

<font size="+0.5" ><b>Lựa chọn các bins như sau `16-25`, `26-30`, `31-60` và lưu vào cột mới là `Nhóm tuổi`
</b></font>

<font size="+1" color=blue><b>Bước 2: Tách cột ngành nghề thành các ngành nghề cụ thể
</b></font>

<font size="+1" color=blue><b>Bước 3: Tạo bảng để tính số lượng cho mỗi `Ngành nghề` và `Nhóm tuổi`

</b></font>

<div>

<table border="1" class="dataframe">
<caption><font size="4"><b>Bảng ngành nghề theo nhóm tuổi</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th>Nhóm tuổi</th>
      <th>16-25</th>
      <th>26-30</th>
      <th>31-60</th>
    </tr>
    <tr>
      <th>Ngành nghề</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>An ninh - Bảo vệ</th>
      <td>1</td>
      <td>15</td>
      <td>42</td>
    </tr>
    <tr>
      <th>An toàn lao động</th>
      <td>1</td>
      <td>8</td>
      <td>11</td>
    </tr>
    <tr>
      <th>Biên phiên dịch</th>
      <td>7</td>
      <td>100</td>
      <td>52</td>
    </tr>
    <tr>
      <th>Bán hàng - Kinh doanh</th>
      <td>250</td>
      <td>934</td>
      <td>464</td>
    </tr>
    <tr>
      <th>Bán sỉ - Bán lẻ - Quản lý cửa hàng</th>
      <td>88</td>
      <td>353</td>
      <td>184</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 4: Trực quan hoá trên 10 ngành nghề có số lượng tuyển nhiều nhất, thêm các giá trị lương trung bình trên mỗi cột màu

</b></font>

![Trực quan hoá Q4](images/3.0-question4.2.png)

<font size="+1.5" color=blue><b>=>Trả lời câu hỏi
</b></font>

Biểu đồ cho thấy Nhóm tuổi từ 26-30 được tuyển dụng nhiều nhất, kế tiếp là từ 31-60, và ít nhất là nhóm tuổi 16-25. Đồng thời có thể thấy mức lương không chêch lệch quá nhiều giữa các nhóm tuổi ở các ngành nghề, và ở các ngành nghề với nhau

<br></br>

<div style="border-radius: 10px; border: 2px solid #51F9F4; padding: 15px; background-color:#c2eeec; font-size: 100%; text-align: left;">
    
<font size="+1" color=#215C67><b>Câu hỏi 5. Cùng một điều kiện, liệu có sự khác biệt trong lương của nam và nữ không? 
</b></font>

<font color="red"><b>Mục đích của câu hỏi: </b></font>

<font color="red">Cho biết liệu có sự phân biệt giới tính nào trong công tác tuyển dụng của các công ty không, nếu có thì cần phải tìm cách khắc phục</font>

<font color="red"><b>Cách trả lời câu hỏi: </b></font>
<font color="red">

- Có 2 bước:

  - _Bước 1_: Lần lượt tách tất cả các hàng dữ liệu khi tại hàng đó và cột cụ thể có chứa hơn 1 giá trị, ví dụ ở cột `Khu vực tuyển` có các hàng có giá trị là nhiều hơn 1 tỉnh, để làm việc này, nhóm sẽ tách các giá trị ở các hàng trong một cột theo giá trị ngăn cách như `/` hoặc `, `. Sau đó sẽ explode theo cột.

  - _Bước 2_: Gom nhóm theo các cột dữ liệu `Khu vực tuyển`, `Ngành nghề`, `Cấp bậc`, `Hình thức làm việc`, `Yêu cầu kinh nghiệm`, `Yêu cầu giới tính`, sau đó so sánh mức lương của nam và nữ. Ở đây nhóm sẽ xem xét ở 5 ngành nghề có lượng tuyển nhiều nhất

  - _Bước 3_: Vẽ biểu đồ cột để so sánh

</font>

<font color="red"><b>Kết quả các bước làm: </b>Biểu đồ cột đôi so sánh mức lương của nam và nữ trong cùng một điều kiện ở 5 ngành nghề có số lượng tuyển nhiều nhất</font>

</div>

<font size="+1" color=blue><b>Bước 1: Tách các cột dữ liệu
</b></font>

<div>

<table border="1" class="dataframe">
<caption><font size=4><b>Bảng dữ liệu sau khi tách</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Khu vực tuyển</th>
      <th>Ngành nghề</th>
      <th>Cấp bậc</th>
      <th>Hình thức làm việc</th>
      <th>Yêu cầu bằng cấp</th>
      <th>Yêu cầu kinh nghiệm</th>
      <th>Yêu cầu giới tính</th>
      <th>Mức lương trung bình</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>9644</th>
      <td>TP.HCM</td>
      <td>Thu mua - Kho Vận - Chuỗi cung ứng</td>
      <td>Cộng tác viên</td>
      <td>Toàn thời gian cố định</td>
      <td>Không</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Nam</td>
      <td>2.500000</td>
    </tr>
    <tr>
      <th>8616</th>
      <td>TP.HCM</td>
      <td>Khách sạn - Nhà hàng - Du lịch</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Thực tập</td>
      <td>Không</td>
      <td>Chưa có kinh nghiệm</td>
      <td>Nam</td>
      <td>3.916667</td>
    </tr>
    <tr>
      <th>6393</th>
      <td>Lâm Đồng</td>
      <td>Nông - Lâm - Ngư nghiệp</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Toàn thời gian cố định</td>
      <td>Trung cấp</td>
      <td>1 năm</td>
      <td>Nam</td>
      <td>12.500000</td>
    </tr>
    <tr>
      <th>10085</th>
      <td>TP.HCM</td>
      <td>Xuất Nhập Khẩu</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Toàn thời gian cố định</td>
      <td>Cao đẳng</td>
      <td>2 năm</td>
      <td>Nữ</td>
      <td>12.500000</td>
    </tr>
    <tr>
      <th>11347</th>
      <td>Điện Biên</td>
      <td>Bảo hiểm</td>
      <td>Chuyên viên- nhân viên</td>
      <td>Toàn thời gian cố định</td>
      <td>Cao đẳng</td>
      <td>1 năm</td>
      <td>Nữ</td>
      <td>15.000000</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 2: Gom nhóm dữ liệu và xem xét lương của nam và nữ ở 5 ngành nghề có số lượng tuyển nhiều nhất
</b></font>

<div>

<table border="1" class="dataframe">
<caption><font size=4><b>Bảng lương trung bình của Nữ giới ở các ngành nghề</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ngành nghề</th>
      <th>Mức lương trung bình</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bán hàng - Kinh doanh</td>
      <td>13.090624</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bán sỉ - Bán lẻ - Quản lý cửa hàng</td>
      <td>13.288988</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chăm sóc khách hàng</td>
      <td>12.658983</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hành chính - Thư ký</td>
      <td>10.811160</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kế toán</td>
      <td>11.023240</td>
    </tr>
  </tbody>
</table>
</div>

<div>

<table border="1" class="dataframe">
<caption><font size=4><b>Bảng lương trung bình của Nam giới ở các ngành nghề</b></font></caption>
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Ngành nghề</th>
      <th>Mức lương trung bình</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bán hàng - Kinh doanh</td>
      <td>13.090624</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bán sỉ - Bán lẻ - Quản lý cửa hàng</td>
      <td>13.288988</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Chăm sóc khách hàng</td>
      <td>12.658983</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hành chính - Thư ký</td>
      <td>10.811160</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kế toán</td>
      <td>11.023240</td>
    </tr>
  </tbody>
</table>
</div>

<font size="+1" color=blue><b>Bước 3: Trực quan hoá
</b></font>

![Trực quan hoá Q5](images/3.0-question5.png)

<font size="+1" color=#215C67><b>Nhận xét:
</b></font>

- Có thể thấy ở 5 ngành nghề có số lượng tuyển lớn nhất, dù không chênh lệch nhiều, nhưng lương của nam giới cao hơn nữ giới trong cả 5 ngành

- Việc cao hơn trong cả 5 ngành không thể hiện rõ được vấn đề mà câu hỏi đặt ra, nên chúng ta sẽ xem xét tiếp rằng trong các ngành còn lại liệu lương của nam giới có cao hơn nữ giới trong tất cả các ngành không

<font size=3><b>Xem xét ở tất cả các ngành</b></font>

Số lượng ngành nghề nam giới có lương cao hơn nữ giới: 30

Số lượng ngành nghề nữ giới có lương cao hơn nam giới: 23

<font size="+1" color=#215C67><b>Nhận xét:
</b></font>

- Vẫn có nhiều ngành nghề mà trong đó lương của nữ giới cao hơn nam giới trong cùng điều kiện tuyển dụng (23/53 ngành, gần một nửa số ngành thu thập được trong dữ liệu). Có thể thấy rằng gần như không có sự phân biệt giới tính trong công việc ngày nay.

<font size="+1.5" color=blue><b>=>Trả lời câu hỏi
</b></font>

- Ngày nay, phân biệt giới tính trong công việc gần như là không còn tồn tại

### 4. Mô hình hóa dữ liệu

- Ở phần này nhóm áp dụng những mô hình học máy đơn giản của thư viện sci-kit learn để tạo ra mô hình dự đoán mức lương.
  4.1. Tiền xử lý dữ liệu
  ![Tiền xử lý dữ liệu](images/4.0-models-preprocessing.png)
- Nhóm sẽ tiền xử lý những cột multi label bằng cách đối với Khu vực tuyển, nhóm sẽ nhân thành nhiều dòng, mỗi dòng ứng với mỗi khu vực tuyển.
- Đối với cột ngành nghề, nhận thấy chỉ có tối đa 3 ngành nghề trong 1 cột dữ liệu nhóm sẽ thành ra thành 3 cột tương ứng: `Ngành nghề chính, Nghề liên quan 1, Nghề liên quan 2.`
- Sau cùng đổi tên các cột sang kiểu tiêu chuẩn tiếng anh để phân tích tiếp.

  4.2.Trích xuất đặc trưng

- Không phải cột nào cũng ảnh hưởng đến cột Lương trung bình. Do đó phải qua các bước để đánh giá những cột nào có thể ảnh hưởng đến cột mục tiêu. Dựa vào mức kỳ vọng p-value để đánh giá xem cột đó có ảnh hưởng đến cột mục tiêu hay không.

- Đổi với những cột có dữ liệu phân loại, Nhóm sẽ áp dụng `ANOVA` để đánh giá xem cột đó có ảnh hưởng đến cột mục tiêu hay không.

![Xử lý cột dữ liệu phân loại](images/4.0-cat_col_affect.png)

- Kết quả có 10/11 cột ảnh hưởng đến mức lương, chỉ có cột loại công ty thì không ảnh hưởng.

-Đối với những cột số nhóm chạy mô hình `Pearson` để đánh giá xem cột đó có ảnh hưởng đến cột mục tiêu hay không.
![Xử lý cột dữ liệu số](images/4.0-num-col-affect.png)

- Kết quả chỉ có cột số lượng tuyển không ảnh hưởng đến cột mục tiêu.

  4.3. Chuẩn bị dữ liệu
  ![Chuẩn bị dữ liệu](images/4.0-data-transformation.png)

  4.4. Mô hình hóa
  ![Xây dựng mô hình](images/4.0-models-building.png)

  4.5. So sánh kết quả các mô hình
  ![So sánh kết quả các mô hình](images/4.0-models-comparation.png)

- Đánh giá mô hình

![Đánh giá mô hình](images/4.0-evaluation.png)

- Nhận xét kết quả:
  ![Nhận xét kết quả](images/4.0-models-comment.png)

### 5. Triển khai mô hình

Nhận thấy mô hình `Extra Tree` có hiệu suất tốt nhất nên chúng em quyết định áp dựng model này vào phần triển khai để áp dụng vào thực tế.

- Lưu dữ liệu lại vào `models/Extra Tree.pkl`. Đồng thời cũng lưu những nhãn dữ liệu mã vào vào file `models/*.pkl` để khi triển khai mô hình có thể chuyển đổi dữ liệu về dạng số để dự đoán.

- Nhóm em quyết định triển khai thư mục bằng Flask để tạo nên trang web có thể tương tác và đưa ra dự đoán mức lương cho người dùng.
- Trang web có chức năng chính là: Cho người dùng chọn những Option mà nó đã được lưu vào models trước đó `Những cột phân loại` cũng như được nhập `Các cột số` để dự đoán mức lương mà người dùng có thể offer khi tuyển dụng hoặc thương lượng với nhà tuyển dụng của mình.
- Cách chạy: Vào trực tiếp thư mục `Model Deployment` và chạy câu lệnh `python app.py` để chạy chương trình, sử dụng trình duyệt web vào port `http://127.0.0.1:5000/` để xem kết quả
- Kết quả:
  ![Trang web](images/4.0-extra-tree-deployment_1.png)
  ![Trang web](images/4.0-extra-tree-deployment_2.png)

## Tác giả

- [Nhóm 22](https://github.com/HungLVT/NMKHDL.git)

## Liên hệ

- [Nguyễn Văn Quang Hưng]
- [Huỳnh Trí Nhân]
- [Chiêm Bỉnh Nguyên]
- [Huỳnh Thị Kiều Hoa]
