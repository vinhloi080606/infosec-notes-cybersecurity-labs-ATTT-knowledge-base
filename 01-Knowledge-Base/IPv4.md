# IPv4 là gì?
    - IP là giao thức - địa chỉ nhà -> các thiết bị có kết nói internet kết nối nhận diện và giao tiếp với nhau
    - nhận biết cách gói tin di chuyển, cách rà quét mạng, giả mạo địa chỉ, quy tắc tường lửa
# cấu trúc IPv4 
    - có 32 bit, chia đều làm 4 phần (octet) mỗi phần có 8 bit. hiển thị dưới dạng thập phân cách nhau bằng dấu .
        - ví dụ : 192.168.1.1 (11000000.10101000.00000001.00000001)
    - có 2 thành phần 
        - Network ID (phần mạng): toàn bộ host ID tại 1 khu vực sẽ gom vào network ID -> không cần xử lý từng Host mà gom Host thành 1 bó để dễ quản lý 
            - gồm có private và public
        - Host ID (phần thiết bị): id của thiết bị kết nối vào network ID -> id của điện thoại, laptop, TV
        -> có 1 ranh giới gọi là Subnet Mask
        -> cấu trúc đi từ Host ID đến private Network đến public network. đi từ thiết bị riêng (điện thoại, laptop)-> mạng nội bộ (wiffi) -> các nhà mạng (vittel,vinaphone,...)-> các trang web và ngược lại
        - ứng dụng : trong một công ty chia mạng (network ID) ra để có thể bảo vệ hoặc truy suất khi có sự cố. Không vì 1 máy mà ảnh hưởng cả công ty.
        - luôn mất đi 2 Host ID vì 0 (gọi tên toàn bộ mạng) và 255 (gửi cho tất cả mọi người trong mạng)/
# Subnet Mask là gì?
    - Subnet Mask là 1 bộ lọc để chia Network ID và Host ID làm đôi
        - các bit 1 -> Network ID
        - các bit 0-> Host ID
    - một địa chỉ như 192.168.1.1 sẽ có kèm 1 Subnet Mask như 255.255.255.0 (viết gọn là /24-> 24 số 1)
        - 
# số địa chỉ IPv4 
    - có 2^32 tương đương khoảng 4,3 tỷ địa chỉ độc nhất-> đã cạn kẹt
    -> giải quyết bằng mạng cục bộ và IPv6 


 