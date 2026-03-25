# OBS Moving Background

OBSブラウザソースとして利用できる「動的ライブ配信背景」です。
HTML/CSS/JSのみで作られており、非常に軽量で外部ライブラリを一切使用していません。GitHub Pages等でホストして即座に利用可能です。

## 機能
- **テーマ切替**: 雑談用（Talk）とゲーム配信用（Game）の2種類のテーマを搭載
- **JST時計**: 日本時間（JST）で日付・デジタル時計を表示
- **カスタム可能**: URLパラメータを使って配信者名やテーマカラーのカスタマイズが可能
- **自由なレイアウト**: 配信者名と時計の配置を画面4隅のいずれかに自由に指定可能
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
| `namePos` | 配信者名の位置 | `左上`, `右上`, `左下` (デフォルト), `右下` (または `top-left` 等) |
| `timePos` | 時計の位置 | `左上`, `右上` (デフォルト), `左下`, `右下` (または `top-left` 等) |

### 💡 表示位置と重複時の仕様について
- **デフォルト配置**: パラメータ指定がない場合、配信者名は「左下」、時計は「右上」に表示されます。
- **位置の重複（優先度）**: 配信者名と時計の表示位置が同じ（被った）場合、**配信者名が優先して表示され、現在日時は自動的に非表示**になります。
- **表示幅の自動最適化**: 配置位置が被らない場合（例：左上と右下など高さが違う場合）、配信者名が長くても画面端まで制限なくゆったりと表示できるように横幅が自動調整されます。

### 💡 組み合わせ例（ローカルファイルの場合）
`file:///C:/path/to/index.html?theme=game&name=Player1`

### 💡 組み合わせ例（GitHub Pages等で動かす場合）
- **トーク用（デフォルト）**: 
  `https://username.github.io/stream-background/`
- **ゲームテーマを使用**: 
  `https://username.github.io/stream-background/?theme=game`
- **配信者名を表示する**: 
  `https://username.github.io/stream-background/?theme=talk&name=VTuberUser`
- **配信者名を「左上」、時計を「右下」に配置する**: 
  `https://username.github.io/stream-background/?name=VTuberUser&namePos=左上&timePos=右下`
- **ゲームテーマでアクセントカラーを赤（#FF0000）に変更**: 
  `https://username.github.io/stream-background/?theme=game&custom=%23FF0000`

## 技術情報
- HTML5 Canvas APIを利用した60fpsアニメーション
- CSS Keyframesによる軽量な背景効果
- JavaScript `Date` APIからの `Asia/Tokyo` 取得による強制JST表示
