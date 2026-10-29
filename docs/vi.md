# Cthangover: Murakami — một tuyến truyện của trò chơi chính

Mod này thêm vào Cthangover một tuyến truyện: có gì đó lảng vảng trong thị trấn, và đi theo nó sẽ dẫn tới cuộc gặp Murakami. Nó mang theo kịch bản của cuộc gặp, Murakami với tư cách nhân vật cùng chân dung và bộ biểu cảm, một nhiệm vụ trong nhật ký, và các trận chiến. Tuyến này thuộc về trò chơi Cthangover và cần cốt truyện gốc (`cthangover_game`) mới chạy được.

Trang này mô tả tuyến gắn vào trò chơi ra sao và bắt đầu thế nào; những gì xảy ra sau đó để dành cho người chơi.

## Tuyến bắt đầu ra sao

Khi Marao tới lối vào thị trấn, một tiếng gầm gừ vang lên từ bóng tối và người chơi chọn quay về nhà hay ghé kiểm tra con hẻm:

![Lối vào thị trấn ban đêm: dòng văn bản “[Từ bóng tối vang lên một tiếng gầm gừ trầm]” với hai lựa chọn Về nhà và Kiểm tra con hẻm.](assets/growl.jpg)

Chọn kiểm tra con hẻm sẽ khởi động nhiệm vụ **Gặp Murakami**, và mục ghi đầu tiên xuất hiện trong nhật ký:

![Nhật ký với nhiệm vụ đang làm Gặp Murakami và mục ghi “Tôi gặp một con sói hoang trong thành phố; nó đang cố vào một ngôi nhà khóa cửa”.](assets/journal.jpg)

## Tuyến gắn vào cốt truyện gốc thế nào

Mod không thay đổi tệp nào của trò chơi gốc. Nó thêm kịch bản vào các cảnh sẵn có, và trò chơi chọn cảnh để chơi theo độ ưu tiên và điều kiện:

```scenario
scene: town_entry
priority: 10
condition: MeetingMurakamiQuest.notHasTag("wolf_battle")
```

- Kịch bản mở đầu thuộc về cảnh `town_entry` với độ ưu tiên 10, nên trong khi điều kiện của nó còn đúng, nó được chọn thay cho các kịch bản thường của thị trấn.
- Mỗi bước tiếp theo của tuyến là một kịch bản khác của `town_entry` với độ ưu tiên cao hơn (20, 30), điều kiện của nó dựa trên các thẻ của nhiệm vụ `MeetingMurakamiQuest`. Bước cuối diễn ra trong nhà (`home_vestibule`).
- Các trận chiến bắt đầu bằng `battle.init` trên hệ thống chiến đấu của nền tảng; kết quả được ghi ngược lại thành thẻ nhiệm vụ, nhờ đó kịch bản kế tiếp biết chuyện gì đã xảy ra.
- Khi tuyến kết thúc, các điều kiện của nó không còn đúng và thị trấn lại chơi những kịch bản thường của mình.

Mod có những gì:

- `scenarios/murakami/meeting/` — bốn kịch bản của cuộc gặp;
- `quests/quests.json` — nhiệm vụ với ba mục ghi nhật ký;
- `characters/player/murakami.json` — Murakami với tư cách nhân vật, kèm hình;
- `avatars/murakami/` — biểu cảm của cô cho hội thoại;
- ảnh nền của cuộc gặp trong `backgrounds/town/meetingmurakami/`;
- văn bản bằng bảy ngôn ngữ trong `locale/`.

## Tắt tuyến này

Có thể bỏ tuyến ra khỏi bộ sưu tập của trò chơi: thị trấn khi đó chỉ chơi kịch bản của chính mình và nhiệm vụ không bao giờ xuất hiện.

## Vấn đề đã biết

- Hai biểu cảm của Marao mà các kịch bản này dùng, `marao/what` và `marao/relax`, không tồn tại trong trò chơi, nên những dòng đó không hiện chân dung. Trình kiểm tra báo chúng là `REF_NOT_FOUND`.
