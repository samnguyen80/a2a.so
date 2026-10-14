# BRIEF — a2a.so

Trạng thái: chốt 2026-10-14 qua /grillme vòng 1 và 2 (quyết định: `ceo-brain/70-decisions/2026-10-14-a2a-so-site-setup.md`).

## 1. Site này là gì

a2a.so là hub kiến thức độc lập về giao thức A2A (Agent2Agent): A2A là gì, vì sao nó tồn tại, ai đang dùng, số liệu hệ sinh thái cập nhật tự động, use case, và các repo/thư viện hữu ích để build agent nói chuyện với agent.

- Mục tiêu: trở thành nguồn tham khảo trung lập mà dev và agent hay trích dẫn. Uy tín quay về Avada và Sam qua trang About, không qua CTA bán hàng.
- Người đọc: dev và kỹ sư AI đang build multi-agent, PM/CTO đánh giá A2A, và chính các AI agent (site phải đọc được bằng máy).
- Chủ sở hữu: Avada Group. Tác giả: Sam Nguyen.
- Bắt buộc ở footer mọi trang: "Independent community resource. Not affiliated with the A2A Project, the Linux Foundation or the Agentic AI Foundation." kèm link https://a2a-protocol.org.

## 2. Ngôn ngữ

- Tiếng Anh trước, ở root (`/what-is-a2a`).
- Dựng sẵn khung i18n: nội dung nằm trong `src/content/en/`, route tiếng Việt sau này là `/vi/...` với `src/content/vi/`. Chưa dịch ở phase này. Trang thiếu bản `vi` thì không sinh route `vi` (không fallback lẫn ngôn ngữ).

## 3. Sitemap và nội dung từng trang

| Route | Trang | Nội dung chính | Nguồn dữ liệu |
|---|---|---|---|
| `/` | Giới thiệu A2A (trang chủ) | A2A trong 1 câu, 3-4 con số live, sơ đồ agent ↔ agent, lối vào các mục | `data/stats.json` |
| `/what-is-a2a` | A2A là gì | Agent Card (`/.well-known/agent-card.json`), task, message, part, transport (JSON-RPC, gRPC, REST), những gì mới ở v1.0, so sánh A2A và MCP | spec a2a-protocol.org |
| `/why-a2a` | Vì sao A2A tồn tại | Bài toán agent của nhiều vendor không nói chuyện được với nhau; giá trị cho con người (ít khoá vendor, ghép agent tốt nhất) và cho agent (tự khám phá, uỷ thác, hợp tác có auth) | |
| `/companies` | Công ty đang dùng | Chia nhóm: đồng sáng lập dự án, nền tảng cloud hỗ trợ, framework tích hợp sẵn, bên ủng hộ đã công bố. Mỗi dòng có link nguồn và ngày | `data/companies.yaml` |
| `/stats` | Số liệu live | Star repo chính thức, lượt tải SDK (PyPI, npm), số release, số repo cộng đồng; dòng "updated X hours ago" | `data/stats.json` |
| `/use-cases` | Use case | 6-8 use case, mỗi cái có ví dụ thật và link | |
| `/repos` | Repo và thư viện | SDK chính thức, framework hỗ trợ A2A, công cụ test/inspect, registry, sample. Star cập nhật tự động | `data/repos.yaml` + `data/stats.json` |
| `/people` | Người dẫn dắt hệ sinh thái A2A | 5-10 người, vai trò, link nguồn công khai. Không gán câu nói không có nguồn | `data/people.yaml` |
| `/about` | Về a2a.so | Ai làm, vì sao, disclaimer, liên hệ | |
| `/about/sam` | Về Sam Nguyen | Agent viết nháp từ nguồn công khai (LinkedIn, samnguyen.work, bài đã đăng), chạy humanize-site, Sam duyệt trước khi publish | nguồn công khai |
| `/about/avada` | Về Avada | Số khách hàng (không doanh thu), số app, Avada sở hữu a2a.so | số từ nexus, xem mục 6 |
| `/about/founders` | Co-founder Avada | Sam Nguyen (Founder & CEO) và Thomas — Nguyễn Tuấn Anh (Co-founder & CTO). Chỉ hai người này | Sam chốt |

Kèm theo: `/llms.txt`, `/llms-full.txt`, bản `.md` cho từng trang, `sitemap.xml`, `robots.txt`, JSON-LD.

Dữ liệu nghiên cứu ban đầu (có link nguồn, đã đánh dấu mức kiểm chứng): `research/a2a-facts-2026-10-14.md`.

## 4. Techstack — copy stack avada.io

avada.io không dùng Nextra (đã kiểm `31-websites/avada.io/package.json`: Next.js 16.2.6, React 19.2.4, `next.config.ts` có `output: 'export'`). Sam chốt dùng đúng stack đó.

- Next.js 16 App Router, `output: 'export'`, TypeScript, Tailwind (theo `postcss.config.mjs` của avada.io).
- Nội dung MDX/markdown trong `src/content/<lang>/`, đọc bằng `gray-matter`.
- Lấy lại các script postbuild từ `31-websites/avada.io/scripts/`: `gen-md.ts`, `gen-llms-full.ts`, `generate-sitemaps.ts`, `inject-jsonld.ts`, `check-md.ts`. Chỉ lấy phần dùng được, bỏ phần riêng của avada.io (crawl, legacy redirects, Cloudflare purge).
- Package manager: theo avada.io (npm, có `package-lock.json`).

## 5. Số liệu live (cron 6 giờ)

GitHub Actions `schedule: '0 */6 * * *'` chạy `scripts/fetch-stats.ts`: gọi API → ghi `data/stats.json` (kèm `updatedAt`) → build → deploy. API lỗi thì giữ số cũ, không làm hỏng build.

| Chỉ số | Nguồn | Auth |
|---|---|---|
| Star, last push các repo `a2aproject/*` và repo trong `data/repos.yaml` | `api.github.com/repos/{owner}/{repo}` | `GITHUB_TOKEN` của Actions |
| Release mới nhất của spec | `api.github.com/repos/a2aproject/A2A/releases` | như trên |
| Lượt tải `a2a-sdk` (PyPI) | `pypistats.org/api/packages/a2a-sdk/recent` | không |
| Lượt tải `@a2a-js/sdk` (npm) | `api.npmjs.org/downloads/point/last-week/@a2a-js/sdk` | không |
| Số repo cộng đồng | `search/repositories?q=a2a+agent2agent+in:name,description,topics` | token |

Không dùng `topic:a2a` (nhiễu, kéo cả repo không liên quan). NuGet, crates.io, Maven để phase sau vì chưa kiểm API.

## 6. Về Avada — số khách hàng

Tính từ nexus.avada.net (snapshot 2026-10-14, lọc trùng theo shop domain trên 36 app), làm tròn lên hàng nghìn, KHÔNG nói doanh thu:

- Đang active (còn ít nhất 1 app Avada): 177.814 → 178,000+
- Từng phục vụ (đã từng cài): 1.014.559 → 1,015,000+

Sam chốt chỉ dùng một số: "1,015,000+ merchants served" (tính cả shop đã gỡ app, chưa loại shop test/bot). Không đưa số active lên site.

## 7. Deploy

- GitHub Actions → GitHub Pages, repo public `github.com/samnguyen80/a2a.so`, branch `main`.
- Custom domain `a2a.so` (Namecheap, nameserver Cloudflare): file `public/CNAME`, bản ghi A/AAAA trỏ IP GitHub Pages, ban đầu để DNS-only để GitHub cấp cert, bật "Enforce HTTPS". Sửa DNS là thao tác ra ngoài, báo Sam trước khi làm.
- `basePath` rỗng (custom domain ở root).

## 8. Quy tắc nội dung

- Mọi khẳng định về công ty, con người, số liệu có link nguồn. Không có nguồn thì không đưa.
- Ngày tháng không chắc thì ghi theo tháng (vd A2A vào AAIF "August 2026" — các nguồn lệch ngày 17/20/27).
- Không có case study khách hàng có số liệu: không bịa, ghi đúng mức "announced support".
- Nội dung agent viết phải chạy skill `humanize-site` trước khi commit (note gốc ghi `/humanizer`, skill đang có tên `humanize-site`).
- Không commit dữ liệu nội bộ Avada (repo public).

## 9. Định nghĩa xong (phase 1 build)

1. `npm run build` xanh, `out/` có đủ route ở mục 3 + llms.txt + sitemap.
2. `scripts/fetch-stats.ts` chạy thật ra `data/stats.json` có số.
3. Workflow deploy chạy xanh, https://a2a.so mở được với HTTPS.
4. Gate verify: `bun /Volumes/SamDisk/ceo-brain/scripts/verify.ts` exit 0.
5. Nội dung từng trang là phase 2 (/grillme riêng); phase 1 chỉ cần khung và nội dung tối thiểu có nguồn.
