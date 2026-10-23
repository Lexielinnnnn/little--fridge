# Little Fridge / 小小冰箱

A bilingual, browser-based fridge inventory and cooking diary. Built with plain HTML, CSS, and JavaScript. No npm installation, API key, database, or paid AI is required.

## Features

- Chinese / English interface, with saved language preference.
- Editable fridge name, synchronized with the fridge illustration.
- Fridge, freezer, and prep zones, each with its own Add button.
- Drag cards between zones without confirmation; the entire quantity moves.
- Edit quantities, units, purchase dates, and storage dates.
- Food-name keyword matching for emoji icons (not AI photo recognition).
- Upload, preview, enlarge, replace, and remove food photos.
- Cook from the prep area: deduct actual quantities and save a meal photo.
- Cooking diary with date tabs and add/edit/delete entries.
- Custom reminder rules and calendar (.ics) export.
- In-page confirmation dialogs and JSON backup / restore.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | Page structure and script entry points |
| `style.css` | Responsive layout, colors, and components |
| `app.js` | Inventory, photos, diary, reminders, and local persistence |
| `i18n.js` | Interface translation and fridge naming |
| `.nojekyll` | Serve the project as a plain static GitHub Pages site |
| `.gitignore` | Keep local files and backups out of Git |

Keep all four application files together at the repository root. There is no build step.

## Run locally

Open `index.html` in a browser for a quick preview. For a consistent local origin, run this from the project folder:

```bash
python3 -m http.server 8000
```

Then visit http://localhost:8000. On Windows, `py -m http.server 8000` may be used instead. Press Ctrl+C to stop.

## Publish using GitHub Pages (no terminal needed)

1. Create a GitHub repository, for example `little-fridge`. Choose **Public** when using GitHub Free.
2. Extract the downloaded ZIP. Upload the files **inside** `little-fridge-github` using **Add file → Upload files**. `index.html` must be at the repository root, not inside another folder. Upload the source files, not the ZIP.
3. Commit the upload to `main`.
4. Open **Settings → Pages**.
5. Under **Build and deployment**, choose **Deploy from a branch**.
6. Select **main** and **/(root)**, then click **Save**.
7. Wait for deployment to complete. Use the live URL shown on the Pages settings screen.

A project URL normally looks like `https://YOUR-USERNAME.github.io/little-fridge/`. This is a format example, not an already-published site.

Share the live URL with others. They can use the site without installing code or signing into the app. Updating files in the selected branch triggers another deployment.

Official instructions:
- https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

## Optional: upload with Git

Create an empty repository first, then run inside this folder. Replace `YOUR-USERNAME` with your GitHub username.

```bash
git init
git add .
git commit -m "Add Little Fridge website"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/little-fridge.git
git push -u origin main
```

Configure Pages as described above. GitHub authentication must already be configured on your computer.

## Where users' data lives

Food records, images, settings, and diary entries are saved in `localStorage` under `little-fridge-v1`, in the browser that opens the website. There is no application server or account system, and the app does not upload these records to GitHub.

- Different browsers/devices have separate inventories. Two people sharing the same browser profile and site origin share that local inventory.
- Clearing browser site data, private browsing, or storage eviction can remove records.
- Moving from a downloaded HTML file to the hosted website does not automatically migrate data. Export a backup from the old version, then import it on the new website.
- GitHub project sites under the same hostname share an origin. Avoid deploying another app with the same storage key on that hostname.
- Photos are resized to at most 800 pixels on their longest side and stored as compressed JPEG. Browser storage is limited, so periodically export backups.
- Backup files include photos and personal records. Do not commit them to your repository.

## Reminders: current behavior

The website shows a reminder badge once the purchase-based first reminder date is reached. It does not send background push notifications and does not track delivered reminder counts. The repeat interval and number of reminders are used to generate calendar events.

Calendar export creates future events at 10:00 AM in the exporting device's timezone, with an alert at the event time. Import the `.ics` file into a compatible calendar and enable that calendar's notifications. Past events are skipped. Calendar compatibility and notification settings determine delivery. If a food is eaten, deleted, or rescheduled, remove its old calendar events manually; they do not synchronize with the website.

Reminders are not food-safety or expiry assessments.

## What would require a backend

Account sign-in, cross-device sync, shared household fridges, durable cloud photo storage, and automatic push notifications while the website is closed are not included. They require additional backend storage, access controls, and (for push) subscriptions plus a server-side scheduler. Publishing on GitHub Pages alone does not add these features.

## Verification and current limits

JavaScript syntax and targeted logic checks were run during development. Full browser/device QA has not been completed. Desktop drag-and-drop is implemented; on touch devices, open a card and change its storage zone if dragging is unavailable. The responsive layout and image flows should be tested on the browsers you intend to support before a broader launch.

Interface language switching preserves user-authored food names, diary text, and fridge names. Icons use a finite keyword list; uncommon foods may use a generic category icon.

## 中文快速说明

这是完整的静态网站源码，无需安装 npm 或填写 API key。

发布方法：解压 → 把文件上传到 GitHub 仓库根目录 → Settings → Pages → Deploy from a branch → main + /(root) → Save。发布完成后，把 Pages 显示的网址发给别人即可。

每个人的数据保存在自己使用的浏览器里，不会自动同步到其他设备。同一浏览器配置下打开同一网站会共用记录。清除浏览器数据可能导致记录丢失，请导出备份。从旧 HTML 文件换到线上网站时，请先导出，再在新网站导入。

当前没有登录、共享冰箱、云端同步或关闭网页后的自动推送。日历提醒需要用户导入并允许日历通知。这里只记录购买时间和提醒规则，不判断食物是否安全。
