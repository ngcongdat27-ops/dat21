---
name: commercial-policy-compliance
description: Soạn thảo bộ văn bản thương mại (Điều khoản sử dụng, Chính sách bảo mật, Chính sách thanh toán/hoàn tiền, Miễn trừ trách nhiệm) và kiểm toán đối chiếu sự thật giữa cam kết pháp lý với mã nguồn thực tế trước khi phát hành phần mềm thương mại.
---

# Commercial Policy, Privacy & Compliance Skill

## 1. Phạm vi & Ranh giới Tuyệt đối (Guardrails)
- **Thời điểm kích hoạt:** CHỈ áp dụng ở các cột mốc phát hành thương mại (Commercial Release, thay đổi bảng giá/luồng thanh toán, hoặc đóng gói bộ cài `.exe`/`.apk`). KHÔNG tự chạy ở các lượt `/hotfix` hoặc sửa lỗi kỹ thuật nhỏ.
- **Cấm bịa đặt văn bản luật:** Tuyệt đối KHÔNG tự trích dẫn số hiệu Luật, Nghị định, Thông tư cụ thể (Việt Nam hay quốc tế) nếu không tra cứu nguyên văn từ nguồn chính thống. Với các nghĩa vụ pháp định đặc thù (thuế cá nhân/hộ kinh doanh, đăng ký TMĐT, quy định bảo vệ dữ liệu cá nhân), chỉ liệt kê mục cần lưu ý và gắn nhãn `[CHỦ APP TỰ ĐỐI CHIẾU VĂN BẢN LUẬT HIỆN HÀNH]`.
- **Không chặn dây chuyền kỹ thuật:** Vai trò của Skill này là minh bạch hóa rủi ro để người dùng tự quyết định (Informed Consent) và giảm thiểu rủi ro thu thập dữ liệu, KHÔNG thuyết giáo hay tự ý dừng quy trình build.
- **Cấm cam kết phóng đại:** Không dùng các cụm từ đảm bảo tuyệt đối như *"100% an toàn"*, *"không bao giờ bị khóa tài khoản"*, *"bảo hành vĩnh viễn"*, hay *"không bao giờ lỗi"*.

## 2. Bộ 4 Văn bản Thương mại Bắt buộc (`@Sage` thực hiện tại Gate 5)
Khi chuẩn bị đóng gói phát hành thương mại, soạn ngắn gọn, rõ ràng bằng tiếng Việt dễ hiểu (UTF-8 không BOM) và lưu vào `docs/legal/`:

1. **Điều khoản Sử dụng & Miễn trừ Trách nhiệm (`TERMS_OF_SERVICE.md` & bản rút gọn `LICENSE_INSTALLER.txt`):**
   - Nêu rõ phần mềm chạy cục bộ (local) trên thiết bị người dùng theo mô hình License Key có thời hạn (không bán gói vĩnh viễn).
   - Quyền & nghĩa vụ: Không chia sẻ Key vượt giới hạn thiết bị, không dịch ngược/can thiệp cơ chế xác thực, người dùng tự chịu trách nhiệm với tài khoản và việc tuân thủ quy định của nền tảng bên thứ ba.
   - Miễn trừ trách nhiệm: Cung cấp theo nguyên trạng ("As-Is"); hỗ trợ vá lỗi hợp lý trong thời hạn gói, không chịu trách nhiệm thiệt hại gián tiếp khi nền tảng bên thứ ba thay đổi cơ chế hoặc hạn chế tài khoản.
   - Quyền điều chỉnh giá/tính năng cho kỳ gia hạn mới (không cắt giảm quyền lợi Key đang hoạt động hợp lệ).

2. **Chính sách Bảo mật Dữ liệu (`PRIVACY_POLICY.md`):**
   - Bắt buộc chia bảng minh bạch **2 cột**:
     * **Dữ liệu chỉ lưu cục bộ trên máy khách (Không bao giờ gửi lên máy chủ):** Cookie phiên đăng nhập, hồ sơ trình duyệt, lịch sử trò chuyện/nhật ký cục bộ, mật khẩu/token cá nhân (Telegram Bot Token, Proxy...).
     * **Dữ liệu tối thiểu gửi lên máy chủ bản quyền:** Mã bản quyền (License Key), mã định danh thiết bị đã băm một chiều (SHA-256 HWID / ANDROID_ID), nền tảng hệ điều hành, tên thiết bị (nếu có), và thông tin đối soát giao dịch thanh toán khi mua gói.
   - Nêu rõ quyền xóa sạch dữ liệu cục bộ khi gỡ ứng dụng và tự hủy liên kết thiết bị theo hạn mức gói.

3. **Chính sách Thanh toán, Dùng thử & Hoàn tiền (`REFUND_AND_BILLING_POLICY.md`):**
   - Quy định rõ luồng mua chuyển khoản tự động (VietQR) và luồng nhận Key dùng thử miễn phí (vượt link rút gọn, khóa cứng thiết bị).
   - **Quy tắc hoàn tiền minh bạch:** Key đã cấp và kích hoạt thành công (đặc biệt gói 1 ngày / dùng thử) không hoàn tiền do đổi ý; hoàn tiền 100% hoặc cấp bù nếu lỗi kỹ thuật từ phần mềm khiến không kích hoạt được trong 24h đầu dù đã hỗ trợ, hoặc chuyển khoản nhầm/thừa/trùng 2 lần.
   - Quy định hạn mức chuyển thiết bị (reset HWID) khớp chính xác bảng `plan_catalog`.

4. **Tích hợp vào Sản phẩm:**
   - Gắn `LICENSE_INSTALLER.txt` sạch lỗi font vào `LicenseFile` hoặc `InfoBeforeFile` của `build/installer.iss`.
   - Đặt dòng xác nhận ngắn kèm liên kết đọc nhanh Điều khoản & Bảo mật ngay tại màn hình Kích hoạt bản quyền (License Gate) và Modal thông tin gói.

## 3. Checklist Kiểm toán Đối chiếu Sự thật (`@Nimbus` thực hiện tại Gate 4)
Trước khi ký `[AUDIT VERDICT: PASSED]` cho bản phát hành thương mại, kiểm tra đủ 8 mục dựa trên bằng chứng mã nguồn thực tế:

- [ ] **1. Khớp dữ liệu gửi đi (Network Truth):** Toàn bộ request ra ngoài KHÔNG gửi Cookie, `browser_profiles`, nội dung tin nhắn, hay `.env` của khách lên máy chủ.
- [ ] **2. Khớp lưu trữ cục bộ (Local Hygiene):** Gói phát hành (`staging`/`dist`/installer) sạch 100% dữ liệu cá nhân chủ app (`.env`, `*.db`, `license.dat`, `logs/`, `browser_profiles/`, khóa bí mật).
- [ ] **3. Khớp thông số gói & chuyển thiết bị:** `max_accounts`, số thiết bị, thời hạn, và việc ẩn nút "Hủy kích hoạt máy này" ở gói dùng thử khớp 100% giữa tài liệu, `plan_catalog` và UI.
- [ ] **4. Không hứa hẹn quá sự thật:** Không có cam kết *"100% không khóa nick"*, *"vĩnh viễn"*, hoặc khẳng định trái thực tế vận hành.
- [ ] **5. Không bịa điều luật:** Không chứa số hiệu Nghị định/Thông tư chưa kiểm chứng; mục cần chủ app tự đối chiếu pháp luật được đánh dấu rõ.
- [ ] **6. Minh bạch thông tin liên hệ thật:** Mọi nút hỗ trợ/email/Zalo/Telegram là kênh thật (không còn link giữ chỗ).
- [ ] **7. Minh bạch xử lý chuyển khoản sai/trùng:** Ghi rõ cách xử lý khi khách ghi thiếu mã đơn hoặc chuyển sai số tiền.
- [ ] **8. Trải nghiệm cài đặt không lỗi font:** Tệp điều khoản nhúng vào trình cài đặt hiển thị rõ ràng, không vỡ ký tự tiếng Việt trên Windows.