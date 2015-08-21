Tim hieu ve KeyStone
# I.Identity Concept

**1.User management**
<ul>
<li>User: Người dùng là con người, những thông tin liên quan như tên, pass user, email...</li>
</ul>
<ul>
<li>Project: Một tenant, group, organization.Khi tạo yêu cầu tới OpenStack service, bạn phải định rõ một project.Ví dụ, nếu truy vấn Compute service cho một danh sách những instance đang chạy, bạn nhận được một list gồm tất cả những instance đang chạy trên project mà bạn truy vấn.</li>
</ul>
<ul>
<li>Domain: Định rõ ranh giới quản lý cho Identity.Mộ domain có thể đại diện cho cá nhân, hội hoặc operator-owner space.Nó gắn những hoạt động quản lý một cách trực tiếp tới hệ thống người dùng.</li>
</ul>
<ul>
<li>Role: Tổ hợp những việc mà user có thể làm trong tenant nhận được.</li>
</ul>
*Note :     Những service cá nhân như Compute và Image được mang ý nghĩa như là role.Trong Identity service, role chỉ đơn giản là một cái tên.
            Một user có thể có nhiều role trong nhiều tenant khác nhau.Một user cũng có thể có nhiều role trong cùng một tenant.*
<ul>
<li>File /etc/[SERVICE_NAME]/policy.json kiểm soát những việc mà user có thể làm tới service nhận được.
<li>File policy.json mặc định trong Compute, Identity, Image chỉ nhận quyền Admin, tất cả những hoạt động khôn yêu cầu quyền admin thì được access bởi bất kỳ user nào có role trong tenant đấy.</li>
Ví dụ : Nếu muốn hạn chế những hoạt động của những user trong Compute, bạn cần tạo ra một role trong Identity sau đó sửa file policy.json trong Compute và gắn role đấy vào.
<li>Trong Compute, trong file policy.json chỉ ra rằng không giới hạn quyền tạo volume và bất kỳ user nào cũng có thể tạo được volume, nếu bạn muốn hạn chế việc đó, bạn cần tạo 1 role trong Identity, ví dụ : compute-user sau đó gắn role đó vào trong file /etc/nova/policy.json.: "volume:create": "role:compute-user" .Lúc này chỉ compute-user mới có quyền tạo volume</li>
</ul>
# 2.Service Management
*Identity Service cung cấp identity, token, catalog và policy, bao gồm : *
<ul>
<li>keystone Web Server Gateway Interface ( WSGI ) service.Có thể chạy trên một WSGI-capable như Apache http để cung cấp Identity service.Service và APIs quản lý chạy như những instace riêng biệt trên WSGI service.
<li>Identity Service functions.Mỗi cái có pluggable back-end mà có thể cho phép sử dụng theo nhiều cách khác nhau cho từng service cụ thể.Phần lớn đều support những back-end cơ bản như LDAP hoặc SQL.
<li>keystone-all: Khởi động cả service và APIs quản lý trên một process duy nhất.Sử dụng federation với keystone không được hỗ trợ.</li>
</ul>
3.Group
Group là tập hợp của nhiều user.Admin có thể tạo một group và add users vào.Có thể gán một role cho từng user và gán một role cho group.Mỗi group ờ trong một domain.
II.Hai cách xác thực cho keystone ( dựa vào  cách user đứa ra identification của họ ) 
1.UUID ( Universally Unique IDentifier
2.PKI ( Public Key IDentification ) 
III.Hợp nhất Idenity với LDAP
1.Idenity back-end chứa thông tin về user, group và danh sách group members.Admin có thể sử dụng users và groups trong LDAP.
2.Assignment back-end.Khi cấu hình OpenStack Identity service để sử dụng LDAP, bạn có thể chia riêng phần xác thực và sự ủy quyền bằng sử dụng assignment feature.Việc hợp nhất assignment back-end với LDAP giúp admin có thể sử dụng projects ( tenant ), role, domains, và role assignment trong LDAP
IV.Token Blinding
