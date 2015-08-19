# Tai Lieu
Tim hieu ve KeyStone
3 Identity Concept
I.User management
-User: Người dùng là con người, những thông tin liên quan như tên, pass user, email...
-Project: Một tenant, group, organization.Khi tạo yêu cầu tới OpenStack service, bạn phải định rõ một project.Ví dụ, nếu truy vấn Compute service cho một danh sách những instance đang chạy, bạn nhận được một list gồm tất cả những instance đang chạy trên project mà bạn truy vấn.
Domain: Định rõ ranh giới quản lý cho Identity.Mộ domain có thể đại diện cho cá nhân, hội hoặc operator-owner space.Nó dùng để gắn thể hiện những hoạt động trực tiếp tới hệ thống người dùng.
