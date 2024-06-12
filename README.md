# vue3-study
Vue3の教科書の学習用リポジトリです

## 環境構築

### VSCode

- Vue Language Features (Volar)
- TypeScript Vue Plugin (Volar)

### プロジェクトの作成と実行

```
npm init vue@latest
cd ${プロジェクト}
npm install 
npm run dev
```

## Notes

### Chap03

- 無名関数内ではthisが指すものが様々に変化し、Vueプロジェクト内でエラーになることが多々。そのためアロー式が推奨されている。
- reactive()関数を使うと複数のデータ（プロパティ）を一つのオブジェクトとして扱える。
- デプロイはnpm run buildでdistに出力したものを使う。ただ、開発中は面倒となるのでnpm run devコマンドが用意されている
### Chap04

- 属性値にデータバインドするには「v-bind:属性の指定」と記述する
- バインドする属性自体を変数指定する場合「v-bind:[属性名]="値"」とする
- style classの適用をbool値を使って動的に設定できる
- v-on:clickでクリックイベント時のふるまい（関数）を設定できる
- v-on:{イベント}="{関数(引数)}"で引数を設定することができる
- ほかの引数と一緒にイベントオブジェクトを使用したい場合は$eventで引数を渡してあげなければならない

### Chap05

- 双方向バインディング
- v-modelで変数を設定すると双方向バインディング
- 片方向の例：「v-on:input」に関数を登録し、イベントから値を反映している
- 例えばTextFieldでv-bindとv-on:inputで同一のテンプレート変数を用いることで双方向バインドを実現できる
    - これをシンプルに記述できるようにしたのが、「v-model」
- コントロールの種類によってv-modelに設定する型が違う
    - Bool
    - Array
    - int or string
- v-htmlでHTMLをレンダリングされるようにできる
- v-onceで一回だけデータバインディングをする
- マスタッシュ構文が一瞬表示される問題
    - 対象のタグにv-cloakディレクティブを記述する
    - v-cloak属性がついているタグはマスタッシュ構文のレンダリングが終わるまでv-cloakのスタイル属性が適用される
    - 今回の例ではdisplay属性をnone(非表示)としている

### Chap06(制御のディレクティブ)

- 基本はv-if
- v-if,v-else-if,v-elseのディレクティブタグの間には別のタグは入れられない
    - 前のタグにv-ifがないとv-else-ifとかがエラーになる
- v-showは常にレンダリングされるため、表示・非表示の切り替えコストが低い。
    - 切り替えがある場合はv-show
    - 切り替えがなくあらかじめ表示非表示が決まっている場合などにv-if
- v-for 「繰り返し変数」 in 「ループするリスト」でイテレーション処理ができる
    - v-bind:keyはキー文字列をバインドします
    - インデックスを取得するにはタプルみたいな形式で「繰り返し変数」を定義する。
- 連想配列ループでのインデックス利用
    - v-for="( 各要素の値, 各要素のキー, インデックス) in ループするリスト"
- key値の工夫
    - v-bind:keyに設定する値は基本的にはオブジェクトのキーがよい
    - ただしcocktailListを同一コンポーネント内で複数回ループ表示をしているので、文字列のプレフィクスを付けて識別できるようにしている
- Mapのループのエイリアス記述
    - v-for="[各要素のキー, 各要素の値] int ループ対象"
- オブジェクトのループは連想配列と同じ
- 複数のタグを繰り返すにはtemplateを使う
    - 6-8の例ではdtタグとddタグにそれぞれkey,valueのペアを繰り返し設定したいため、dtとddをまとめておくタグとしてtemplateを使う
- オブジェクトの配列でループするときは、ループ内変数オブジェクトの特定のkeyをv-bindにセットする
    - v-for="「各要素の値」" in 「ループするリスト」
    - v-bind:key"「各要素の値」.IDに該当するプロパティ"
- Mapにオブジェクトを格納する場合はKeyをそのままv-bindとして使える。
    - id列を冗長に持つことになるかもしれない
    - どちらかというと繰り返しではなく、主キーで一意の値を取得するときに使うとよい
- カウンタ変数を利用したループ構文
    - v-for="カウンタ変数 in 終端の値"
- ループ対象の絞り込み
    - 普通にscript側でfilterしたリストの算出プロパティ（computed）を定義すればよい。
- 配列のデータ操作
    - 以下のようなメソッドがある
        - push(element): 追加
        - pop(): 末尾を除く
        - shift(): 先頭を除く
        - unshift(element): elementを先頭に追加
        - splice(start[,count[, e1[, e2, …]]]): start番目からcount個の要素をe1, e2, …で置換
        - sort(): ソート
        - reverse(): 順番反転
    - refしているリストに対し各操作をするクロージャを定義してアクションに紐づける（v-on）
- Mapのデータ操作
    - 以下のようなメソッドがある
        - clear(): すべて削除
        - delete(): key指定で削除
        - set(): keyとvalueを指定して追加
- Objectのデータ操作
    - プロパティの値を直接代入すればよい
- ObjectのMapのデータ操作
    - リアクティブシステムのおかげで、Objectを変更したらMap全体にも反映される。

### Chap07(スクリプトブロックのバリエーション)
- リアクティブ変数の変化を監視するwatchEffect()
    - 算出プロパティ(computed)には向かない、インターネット上のデータ（API）などを監視する場合？
    - 7-2の例ではsetIntervalで1秒ごとに取得したものを監視する。
    - watchEffectではコールバック関数内のリアクティブ変数すべてが監視対象となる
- watch()
    - 監視対象を明示できる
    - 初回起動時はコールバックを実行しない（変更時のみ）
    - immediate: trueとすると即時起動する。
- Vueのライフサイクル
    1. 起動開始
        - beforeCreate
    2. Vueアプリケーションの初期化処理
        - created
    3. コンポーネントの解析処理
        - beforeMount
    4. レンダリング処理
        - mounted
        - renderTracked（リアクティブ変数への初回アクセス）
    5. ★表示状態★
        - renderTriggerd(リアクティブ変数へのアクセス)
            - beforeUpdate
        1. リアクティブシステムによる再レンダリング処理
            - updated
        - beforeMounted
    6. 非表示処理
        - unmounted
    7. 非表示状態
- defineComponent
    - script setupの前（Vue3.2より前）の書き方
    - これもComposition API
- スプレッド演算子 + toRefs()関数の組み合わせ
    - 従来型の書き方で、上記を使うとreactiveブロックで定義した変数がreturnの際に展開される。
    - setupスクリプトブロックを使用している場合は不要。
- Options API
    - defineComponents()の引数オブジェクトに各プロパティを列挙する
        - data()
        - computed
        - methods
        - updated(): 戻り値⇒ライフサイクルフック
        - watch { 監視対象データプロパティ名(newValue:型, oldValue:型) }
            - watchEffectは存在しない
        
### Chap08(コンポーネント間の連携)
- コンポーネントはsrc/components/にVueファイルを置く
- 「import 別名 from 相対パス」で利用可能になる
- 使用するときは<別名 />でOK
- コンポーネント内のv-modelはコンポーネント内での双方向バインディングを行う
- Propsを子コンポーネントで定義する
    - 個々のPropsをメンバとしたインターフェース
        - 特段理由が抱ければPropsというインターフェース名がよい
    - defineProps<型>()を実行する
        - 上記のインターフェースの型をジェネリクスとする
- Propsの渡し方
    - 普通に属性として渡す
    - スクリプトブロックで用意したテンプレート変数をv-bind:属性名で渡す
- Propsに対してv-forのループ変数をセットすることで、繰り返し子コンポーネントを作成できる
- スクリプトブロックでのPropsデータの利用
    - propsの属性(props.point)への操作はできない（読み取り専用）
    - 一旦別のリアクティブ変数にコピーして利用する
    - ただし親コンポーネントにはそのまま反映することはできない(後述)
- 子コンポーネントから親コンポーネントへの通信にはemitを使う(components-emit-basics参考)
    - interface EmitsでEmitの定義をします
    - 今回はbuttonのv-on:clickにemitの実行をする関数(emit("createNewRand"))を紐づけます
    - 親コンポーネントからv-onでEmit定義に関数を紐づけます（ランダム値生成）
- Emitsで値を渡す
    - emit(ラベル, 値)
        - ラベル： v-onで指定するラベル(v-on:ラベル名)
        - 値：親に渡す変数（例では要素を特定するIDを返している）
    - Emitsのインタフェースの定義にも第２引数の内容を定義しておく必要がある
- v-modelによる子から親への通信
    - 親からはv-modelで渡す(points)とv-bind(値渡し)の時のようにv-onに設定するメソッドは不要になる
    - v-modelとするだけでPropsのデータがEmitによる変更対象となる
    - 構文(emit("update:Prop名", 値))
        - update:を利用したEmit定義があると覚える
- provideとinject
    - provide("Provide名", 値)
    - 値はreactive関数で渡すと全コンポーネントでリアクティブ変数として使用できる
        - ref()だとinject先でvalueプロパティにアクセスするのができない（Typescriptの場合）
    - inject("Provide名") as 型
    - 型アサーションをすることで各プロパティにアクセスできる
