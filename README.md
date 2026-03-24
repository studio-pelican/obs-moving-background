# OBS Moving Background

OBSブラウザソースとして利用できる「動的ライブ配信背景」です。
HTML/CSS/JSのみで作られており、非常に軽量で外部ライブラリを一切使用していません。GitHub Pages等でホストして即座に利用可能です。

## 機能
- **テーマ切替**: 雑談用（Talk）とゲーム配信用（Game）の2種類のテーマを搭載
- **JST時計**: 常に日本時間（JST）で右上にデジタル時計を表示
- **カスタム可能**: URLパラメータを使って配信者名やテーマカラーのカスタマイズが可能
- **OBS最適化**: フルHD想定・透明背景に対応し、配信画面との重ね合わせが容易

## 使用手順（OBSでの設定）

1. OBSの「ソース」から「+」をクリックし、「ブラウザ」を追加します。
2. 追加したブラウザソースのプロパティを開きます。
3. `URL` に、ホストしたページのURL（またはローカルの `index.html`）を入力します。
   - ※ URLパラメータによるカスタマイズについては後述。
4. 解像度サイズを以下のように指定します:
   - **幅**: 1920
   - **高さ**: 1080
5. （必須）**カスタムCSS** の項目に以下を入力します。これによりOBS上で背景が透明に保たれます。
   ```css
   body { margin: 0; background-color: transparent !important; }
   ```
6. 「OK」を押してプレビュー画面に表示されれば完了です。

## URLパラメータによるカスタマイズ

ページのURLの後ろに `?` を付け、以下のパラメータを追加できます。複数のパラメータを指定する場合は `&` で繋ぎます。

| パラメータ | 役割 | 設定値の例 |
| --- | --- | --- |
| `theme` | テーマ変更 | `talk` (デフォルト), `game` |
| `name` | 配信者名などの表記 | `name=MyStreamer` (URLエンコード推奨) |
| `custom` | テーマカラーの変更 | `custom=%23FF00FF` (※ `#`は `%23` にエンコードして指定してください) |

### 💡 組み合わせ例（ローカルファイルの場合）
`file:///C:/path/to/index.html?theme=game&name=Player1`

### 💡 組み合わせ例（GitHub Pages等で動かす場合）
- **トーク用（デフォルト）**: 
  `https://username.github.io/stream-background/`
- **ゲームテーマを使用**: 
  `https://username.github.io/stream-background/?theme=game`
- **配信者名を表示する**: 
  `https://username.github.io/stream-background/?theme=talk&name=VTuberUser`
- **ゲームテーマでアクセントカラーを赤（#FF0000）に変更**: 
  `https://username.github.io/stream-background/?theme=game&custom=%23FF0000`

## 技術情報
- HTML5 Canvas APIを利用した60fpsアニメーション
- CSS Keyframesによる軽量な背景効果
- JavaScript `Date` APIからの `Asia/Tokyo` 取得による強制JST表示
