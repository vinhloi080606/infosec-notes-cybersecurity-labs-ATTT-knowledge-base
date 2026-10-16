# ly thuyết cơ bản về IPv4
# lịch sử IPv4
    - ban đầu IPv4 có 5 lớp (A, B, C, D, E) chỉ có A, B, C phân phát cho thiết bị-> 1 lớp phân cách cố định     
        - lớp A có 8 bit đầu cố định còn lại phân phát =/8 -> chia đến 2^24 địa chỉ host. Dấu hiệu 1-126 ở octet đầu ví dụ (10.xx.xx.xx)
        - lớp B có 16 bit -> /16 còn 2^16 địa chỉ host. dấu hiệu octet đầu từ 128-191 ví dụ (130.xx.xx.xx)
        - lớp c có 24 bit-> /24-> còn 2^8 địa chỉ host. dấu hiệu octet đầu từ 192-223 ví dụ (200.xx.xx.xx)
        - lớp D đi từ 224-239 dùng cho Multicast
        - Lớp E đi từ 240-255 dùng cho nghiên cứu, không cấp cho máy tính
        -->> hạn chế nếu cần cấp cho số lượng máy vừa vượt 2^8 vài bit thì cũng cần xin lên lớp B lãng phí 1 lượng lớn địa chỉ IP -> bị khai trừ và thay thế bởi    CIDR chia một cách tự do 
## IPv4 là gì?
    - IP là giao thức - địa chỉ nhà -> các thiết bị có kết nói internet kết nối nhận diện và giao tiếp với nhau
    - nhận biết cách gói tin di chuyển, cách rà quét mạng, giả mạo địa chỉ, quy tắc tường lửa
## cấu trúc IPv4 
    - có 32 bit, chia đều làm 4 phần (octet) mỗi phần có 8 bit. hiển thị dưới dạng thập phân cách nhau bằng dấu .
        - ví dụ : 192.168.1.1 (11000000.10101000.00000001.00000001)
    - có 2 thành phần 
        - Network ID (phần mạng): toàn bộ host ID tại 1 khu vực sẽ gom vào network ID -> không cần xử lý từng Host mà gom Host thành 1 bó để dễ quản lý 
            - gồm có private và public
        - Host ID (phần thiết bị): id của thiết bị kết nối vào network ID -> id của điện thoại, laptop, TV
        -> có 1 ranh giới gọi là Subnet Mask
        -> cấu trúc đi từ Host ID đến private Network đến public network. đi từ thiết bị riêng (điện thoại, laptop)-> mạng nội bộ (wiffi) -> các nhà mạng (vittel,vinaphone,...)-> các trang web và ngược lại
        - ứng dụng : trong một công ty chia mạng (network ID) ra để có thể bảo vệ hoặc truy suất khi có sự cố. Không vì 1 máy mà ảnh hưởng cả công ty.
        - luôn mất đi 2 Host ID vì toàn 0 (gọi tên toàn bộ mạng) và toàn 1 (gửi cho tất cả mọi người trong mạng)
## Subnet Mask là gì?
    - Subnet Mask là 1 bộ lọc để chia Network ID và Host ID làm đôi
        - các bit 1 -> Network ID
        - các bit 0-> Host ID
    - một địa chỉ như 192.168.1.1 sẽ có kèm 1 Subnet Mask như 255.255.255.0 (viết gọn là /24-> 24 số 1)
        - 
## số địa chỉ IPv4 
    - có 2^32 tương đương khoảng 4,3 tỷ địa chỉ độc nhất-> đã cạn kẹt
    -> giải quyết bằng mạng cục bộ và IPv6 
# kỹ thuật subnetting 
# subnetting là gì?
    - subnetting là kỹ thuật mượn bit từ Host ID-> tạo ra các phần Network ID mới 
    -> chia dãy mạng lớn thành các dãy mạng nhỏ độc lập với nhau-> 1 căn nhà lớn chia phòng ra
# lý do dùng subnnet
    - cô lập và bảo mật: tránh tình trạng một nhân viên ảnh hưởng một công ty bằng cách chia thành các mạng nhỏ ứng mỗi phòng ban -> dữ liệu phải đi qua rounter và firewall tránh đi từ một máy chạy khấp công ty.
    - giảm thiếu rác mạng: một thiết bị tìm thiết bị khác -> gửi bản tin broadcast đến toàn bộ mạng -> chia nhỏ giúp chỉ nhảy trong cụm đã chia thay vì toàn bộ công ty 
    - giảm thiểu lãng phí: thay vì /24 chúng ta có thể /28 để tránh phân phát quá nhiều khi phòng ban ít người
# cơ chế hoạt động
    - ví dụ được cấp 192.168.1.0/24
        - ý nghĩa là 24 bit Network 8 bit Host 
        - muốn có 4 phòng (4 subnet) thì cần mượn  2 bit(2^2=4)-> Network có 26 bit (mask /26) Host còn 6 bit
            - với 6 bit -> 2^6= 64 địa chỉ IP ->có 62 địa có thể sử dụng 
            - với 24 bit ban đầu sẽ thành 4 phòng như sau
                - subnet 1:từ 192.168.1.0 đến 192.168.1.63 
                - subnet 2: từ 192.168.1.64 đến 192.168.1.127
                - subnet 3: từ 192.168.1.128 đến 192.168.1.191
                - subnet 4: từ 192.168.1.192 đến 192.168.1.255
                -> lưu ý các IP đầu và cuối mỗi subnet sẽ không thể kết nối cho máy tính vì nó là Network ID và Broadcast IP
# IP private
    - là địa chỉ được dùng trong mạng LAN ( mạng nội bộ) 
        - đặc điểm
            - miễn phí, tự do cấp phát
            - các công ty khác nhau có thể trung IP này
            - không thể truy cập từ bên ngoài
        - ba dãy tiêu chuẩn
            - A: 10.0.0.0 - 10.255.255.255 - cấp phát nhiều
            - B: 172.16.0.0 - 172.16.255.255 - cấp phát cho trung
            - C: 192.168.0.0 - 192.168.255.255 - cấp phát hộ gia đình và kinh doanh nhỏ
# IP public 
    - là địa chỉ duy nhất dùng trên toàn cầu -> giao tiếp trên môi trường internet
        - đặc điểm
            - là độc nhất 
            - thuê/ mua từ các nhà cung cấp mạng ( viettel, vina,...)
            - bất kể ai dùng internet cũng có thể thấy
# 3 dải private tiêu chuẩn do tổ chức IANA quy định
    - dãy A: từ 10.0.0.0- 10.255.255.255 -> hơn 16.7 triệu IP thường được các tập đoàn đa quốc gia sử dụng ( AWS, gg cloud) hoặc tổ chức giáo dục lớp
    - dãy B: từ 172.16.0.0 - 172.31.255.255-> hơn 1 triệu IP doanh nghiệp tầm trung, hệ thống ảo, Docker container.
    - dãy C: từ 192.168.0.0 -   192.168.255.255-> khoảng 65.536 thường chia nhỏ thành /24 -> wiffi gia đình, cafe, các cửa hàng bán lẻ.
    -->> nếu thấy dãy bắt đầu bằng IP 192.168.xx.xx tấn công -> kẻ tấn công ngồi trong hệ thống hoặc mã độc. còn bắt đầu bằng 10.xx.xx.xx khả năng cao muốn giả mạo thành " người nhà"


# Nat
    - vấn đề là nếu IP Private mà muốn xem YTB nơi IP Public thì như nào?
    - kỹ thuật NAT với cục router là tiếp tân
        - quy trình
            - 1: máy tính gửi yêu cầu đến router
            - 2: yêu cầu từ máy tính đến router, router có 1 IP public
            - 3: router giấu IP private của bạn đi sài IP public của nó gửi yêu cầu đến YTB
            - 4: YTB gửi video về IP public của router, router chuyển về cho IP private
            - lưu ý: khi nhiều người cùng gửi nếu không có kiểm soát sẽ rất loạn nên khi gửi sẽ có 1 cái gọi là PAT để đánh dấu IP nào đưa ra yêu cầu gì.
        -->> người bên ngoài cùng lắm chỉ mò ra được IP public cảu router -> tưởng lửa thô sơ đầu tiên
        -->> tiết kiệm chi phí, 1 router 1 IP public gánh hàng ngang IP private


 