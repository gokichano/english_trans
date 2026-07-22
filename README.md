<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <meta name="description" content="日常英会話の自然な和訳を、個別フィードバック付きで練習できるゲーム" />
  <title>英会話 和訳チャレンジ</title>
  <style>
:root {
  color-scheme: dark;
  --bg: #090b10;
  --panel: #11151d;
  --panel-strong: #171c26;
  --card: #1b2130;
  --line: #2b3342;
  --text: #f7f8fb;
  --muted: #9ba5b5;
  --accent: #7c5cff;
  --accent-hover: #8d73ff;
  --accent-soft: rgba(124, 92, 255, 0.15);
  --success: #43d18b;
  --success-soft: rgba(67, 209, 139, 0.12);
  --warning: #f4bd50;
  --warning-soft: rgba(244, 189, 80, 0.12);
  --danger: #ff6b7d;
  --danger-soft: rgba(255, 107, 125, 0.12);
  --shadow: 0 24px 70px rgba(0, 0, 0, 0.35);
}

* { box-sizing: border-box; }
html { min-height: 100%; background: var(--bg); }
body {
  min-height: 100vh;
  margin: 0;
  font-family: Inter, "Hiragino Sans", "Yu Gothic", "Meiryo", sans-serif;
  color: var(--text);
  background:
    radial-gradient(circle at top right, rgba(124, 92, 255, 0.18), transparent 30%),
    radial-gradient(circle at bottom left, rgba(65, 154, 255, 0.08), transparent 35%),
    var(--bg);
}

button, textarea { font: inherit; }
button { cursor: pointer; }
h1, h2, h3, p { margin-top: 0; }

.app-shell {
  width: min(100% - 32px, 900px);
  margin: 0 auto;
  padding: 48px 0 64px;
}

.site-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 24px;
  margin-bottom: 24px;
}

.eyebrow {
  margin: 0 0 8px;
  color: var(--accent-hover);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.14em;
}

h1 {
  margin-bottom: 10px;
  font-size: clamp(30px, 6vw, 52px);
  line-height: 1.08;
}

.lead, .section-heading p, .question-card p, .result-comment, .final-message { color: var(--muted); }
.lead { max-width: 620px; margin-bottom: 0; line-height: 1.75; }

.header-stats {
  display: grid;
  grid-template-columns: repeat(2, minmax(72px, 1fr));
  flex: 0 0 auto;
  overflow: hidden;
  border: 1px solid var(--line);
  border-radius: 18px;
  background: rgba(17, 21, 29, 0.86);
}

.header-stats div { padding: 12px 16px; text-align: center; }
.header-stats div + div { border-left: 1px solid var(--line); }
.header-stats span { display: block; color: var(--muted); font-size: 11px; }
.header-stats strong { display: block; margin-top: 3px; font-size: 24px; }

.panel {
  padding: clamp(20px, 4vw, 36px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 28px;
  background: rgba(17, 21, 29, 0.92);
  box-shadow: var(--shadow);
  backdrop-filter: blur(16px);
}

.section-heading { margin-bottom: 24px; }
.section-heading h2 { margin: 12px 0 8px; font-size: clamp(25px, 4vw, 36px); }
.section-heading p { margin-bottom: 0; line-height: 1.7; }

.badge {
  display: inline-flex;
  align-items: center;
  min-height: 28px;
  padding: 6px 10px;
  border-radius: 999px;
  background: var(--accent-soft);
  color: #c2b7ff;
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 0.04em;
}

.difficulty-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 12px;
  margin-bottom: 22px;
}

.difficulty-card {
  min-height: 122px;
  padding: 18px;
  border: 1px solid var(--line);
  border-radius: 20px;
  color: var(--text);
  background: var(--panel-strong);
  text-align: left;
  transition: transform 160ms ease, border-color 160ms ease, background 160ms ease;
}

.difficulty-card:hover { transform: translateY(-2px); border-color: #4e5b71; }
.difficulty-card.is-selected { border-color: var(--accent); background: var(--accent-soft); }
.difficulty-name, .difficulty-description { display: block; }
.difficulty-name { margin-bottom: 8px; font-size: 18px; font-weight: 700; }
.difficulty-description { color: var(--muted); font-size: 13px; line-height: 1.6; }

.button {
  min-height: 48px;
  padding: 12px 18px;
  border: 1px solid transparent;
  border-radius: 16px;
  font-weight: 700;
  transition: transform 150ms ease, opacity 150ms ease, background 150ms ease;
}
.button:hover:not(:disabled) { transform: translateY(-1px); }
.button:disabled { cursor: not-allowed; opacity: 0.45; }
.button-primary { color: #fff; background: var(--accent); }
.button-primary:hover:not(:disabled) { background: var(--accent-hover); }
.button-secondary { border-color: var(--line); color: var(--text); background: var(--panel-strong); }
.button-large { width: 100%; min-height: 56px; }

.text-button {
  padding: 8px 4px;
  border: 0;
  color: var(--muted);
  background: transparent;
  font-weight: 700;
}
.text-button:hover { color: var(--text); }
.danger-text:hover { color: var(--danger); }

.countdown-screen { min-height: 360px; display: grid; place-items: center; text-align: center; }
.countdown-screen p { color: var(--muted); }
.countdown-number {
  margin-top: 12px;
  font-size: clamp(92px, 20vw, 160px);
  font-weight: 800;
  line-height: 1;
  animation: count-pop 700ms ease both;
}
@keyframes count-pop {
  0% { opacity: 0; transform: scale(0.6); }
  40% { opacity: 1; transform: scale(1.08); }
  100% { opacity: 1; transform: scale(1); }
}

.question-meta {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
  margin-bottom: 18px;
  color: var(--muted);
  font-size: 14px;
}
.question-meta-left { display: flex; align-items: center; gap: 10px; }

.question-card {
  margin-bottom: 22px;
  padding: clamp(22px, 5vw, 38px);
  border: 1px solid var(--line);
  border-radius: 24px;
  background: linear-gradient(145deg, rgba(124, 92, 255, 0.12), rgba(27, 33, 48, 0.8));
  text-align: center;
}
.question-card p { margin-bottom: 14px; font-size: 13px; }
.question-card h2 { margin: 0; font-size: clamp(25px, 5vw, 38px); line-height: 1.45; }

.answer-area label { display: block; margin-bottom: 10px; font-weight: 700; }
textarea {
  width: 100%;
  resize: vertical;
  min-height: 124px;
  margin-bottom: 12px;
  padding: 16px;
  border: 1px solid var(--line);
  border-radius: 18px;
  outline: none;
  color: var(--text);
  background: var(--panel-strong);
  line-height: 1.75;
}
textarea:focus { border-color: var(--accent); box-shadow: 0 0 0 4px var(--accent-soft); }
textarea:disabled { opacity: 0.7; }
.input-message { margin: -2px 0 12px; color: var(--warning); font-size: 13px; }

.feedback-area { display: grid; gap: 16px; margin-top: 22px; }
.result-panel, .feedback-card, .explanation-card, .report-section, .answer-review-card {
  padding: 20px;
  border: 1px solid var(--line);
  border-radius: 20px;
  background: var(--panel-strong);
}

.answer-review-card { display: grid; gap: 16px; }
.answer-review-section { min-width: 0; }
.original-english-section {
  padding-bottom: 16px;
  border-bottom: 1px solid var(--line);
}
.review-english {
  margin-bottom: 0;
  font-size: clamp(20px, 4vw, 28px);
  font-weight: 800;
  line-height: 1.55;
  word-break: break-word;
}
.answer-comparison-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
}
.user-answer-section,
.correct-answer-section {
  padding: 16px;
  border: 1px solid var(--line);
  border-radius: 16px;
  background: var(--card);
}
.user-answer-section { border-color: rgba(255, 255, 255, 0.1); }
.correct-answer-section { border-color: rgba(124, 92, 255, 0.42); background: var(--accent-soft); }
.review-answer {
  margin-bottom: 0;
  font-size: 17px;
  font-weight: 700;
  line-height: 1.75;
  word-break: break-word;
}
.result-panel { text-align: center; }
.result-panel.is-correct { border-color: rgba(67, 209, 139, 0.42); background: var(--success-soft); }
.result-panel.is-almost { border-color: rgba(244, 189, 80, 0.42); background: var(--warning-soft); }
.result-panel.is-wrong { border-color: rgba(255, 107, 125, 0.42); background: var(--danger-soft); }
.result-title { margin-bottom: 6px; font-size: clamp(28px, 5vw, 42px); font-weight: 800; }
.result-comment { margin-bottom: 0; }

.card-heading-row { display: flex; align-items: flex-start; justify-content: space-between; gap: 16px; }
.feedback-heading { margin: 5px 0 0; font-size: 20px; line-height: 1.5; }
.score-badge {
  flex: 0 0 auto;
  min-width: 62px;
  padding: 7px 10px;
  border-radius: 999px;
  background: var(--card);
  text-align: center;
  font-size: 13px;
  font-weight: 800;
}
.personal-feedback { margin: 18px 0 0; line-height: 1.85; }
.feedback-points { display: grid; gap: 10px; margin-top: 16px; }
.feedback-point { display: flex; gap: 10px; padding: 12px 14px; border-radius: 14px; background: var(--card); line-height: 1.65; }
.feedback-point strong { flex: 0 0 auto; }
.feedback-point.is-good strong { color: var(--success); }
.feedback-point.is-fix strong { color: var(--warning); }
.suggested-rewrite-box {
  margin-top: 16px;
  padding: 16px;
  border: 1px solid rgba(124, 92, 255, 0.42);
  border-radius: 16px;
  background: var(--accent-soft);
}
.suggested-rewrite { margin-bottom: 0; font-size: 18px; font-weight: 800; line-height: 1.75; }

.explanation-card { display: grid; gap: 20px; }
.explanation-card section + section { padding-top: 20px; border-top: 1px solid var(--line); }
.explanation-label { margin-bottom: 7px; color: var(--accent-hover); font-size: 12px; font-weight: 800; letter-spacing: 0.06em; }
.explanation-main { margin-bottom: 0; font-size: 19px; font-weight: 700; line-height: 1.65; }
.explanation-card section p:last-child { margin-bottom: 0; line-height: 1.8; }
.pronunciation { font-weight: 700; }

.action-grid, .finish-actions { display: grid; grid-template-columns: 1fr 1fr; gap: 12px; }

.finish-heading { text-align: center; }
.result-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 12px; margin-bottom: 20px; }
.result-grid-four { grid-template-columns: repeat(4, 1fr); }
.result-stat { padding: 18px 12px; border: 1px solid var(--line); border-radius: 18px; background: var(--panel-strong); text-align: center; }
.result-stat span { display: block; color: var(--muted); font-size: 12px; }
.result-stat strong { display: block; margin-top: 6px; font-size: clamp(25px, 5vw, 38px); }

.report-highlight { margin-bottom: 16px; border-color: rgba(124, 92, 255, 0.45); background: var(--accent-soft); }
.report-section h3 { margin: 0 0 10px; font-size: 20px; }
.report-section p:last-child { margin-bottom: 0; line-height: 1.8; }
.report-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; margin-bottom: 16px; }
.report-list, .next-action-list { margin: 0; padding-left: 1.3em; }
.report-list li, .next-action-list li { padding-left: 4px; line-height: 1.75; }
.report-list li + li, .next-action-list li + li { margin-top: 8px; }
.next-action-section { margin-bottom: 20px; }
.next-action-list li::marker { color: var(--accent-hover); font-weight: 800; }

.trend-toast {
  position: fixed;
  z-index: 20;
  top: 22px;
  right: 22px;
  width: min(390px, calc(100% - 32px));
  padding: 20px;
  border: 1px solid rgba(124, 92, 255, 0.55);
  border-radius: 22px;
  background: rgba(20, 24, 34, 0.97);
  box-shadow: 0 22px 70px rgba(0, 0, 0, 0.5);
  animation: toast-in 260ms ease both;
}
@keyframes toast-in { from { opacity: 0; transform: translateY(-10px); } to { opacity: 1; transform: translateY(0); } }
.trend-toast-head { display: flex; align-items: flex-start; justify-content: space-between; gap: 12px; }
.trend-toast h2 { margin: 3px 0 0; font-size: 20px; line-height: 1.4; }
.trend-kicker { margin-bottom: 0; color: var(--accent-hover); font-size: 12px; font-weight: 800; }
.trend-toast > p { margin: 14px 0 10px; color: var(--muted); line-height: 1.7; }
.trend-toast ul { margin: 0; padding-left: 1.2em; }
.trend-toast li { line-height: 1.6; }
.trend-toast li + li { margin-top: 5px; }
.toast-close { padding: 0 4px; border: 0; color: var(--muted); background: transparent; font-size: 26px; line-height: 1; }
.toast-close:hover { color: var(--text); }

.is-hidden { display: none !important; }

@media (max-width: 720px) {
  .app-shell { width: min(100% - 20px, 900px); padding: 24px 0 40px; }
  .site-header { align-items: stretch; flex-direction: column; }
  .header-stats { align-self: flex-start; }
  .difficulty-grid, .report-grid, .answer-comparison-grid { grid-template-columns: 1fr; }
  .difficulty-card { min-height: auto; }
  .result-grid-four { grid-template-columns: repeat(2, 1fr); }
  .trend-toast { top: 12px; right: 10px; }
}

@media (max-width: 480px) {
  .panel { border-radius: 22px; }
  .question-meta { align-items: flex-start; }
  .action-grid, .finish-actions { grid-template-columns: 1fr; }
  .card-heading-row { flex-direction: column; }
  .score-badge { align-self: flex-start; }
}

</style>
</head>
<body>
  <main class="app-shell">
    <header class="site-header">
      <div>
        <p class="eyebrow">ENGLISH TRANSLATION GAME</p>
        <h1>英会話 和訳チャレンジ</h1>
        <p class="lead">実際の会話で使う英語を、自然な日本語へ変換するトレーニングです。</p>
      </div>
      <div id="header-stats" class="header-stats is-hidden" aria-label="現在の成績">
        <div>
          <span>回答</span>
          <strong id="header-total">0</strong>
        </div>
        <div>
          <span>正解</span>
          <strong id="header-score">0</strong>
        </div>
      </div>
    </header>

    <section id="start-screen" class="screen panel">
      <div class="section-heading">
        <span class="badge">LEVEL SELECT</span>
        <h2>難易度を選択</h2>
        <p>スタート時だけ3カウントします。開始後は、ご自身で終了するまで問題が続きます。</p>
      </div>

      <div class="difficulty-grid" role="group" aria-label="難易度選択">
        <button type="button" class="difficulty-card" data-level="easy" aria-pressed="false">
          <span class="difficulty-name">かんたん</span>
          <span class="difficulty-description">短くて基本的な日常表現</span>
        </button>

        <button type="button" class="difficulty-card is-selected" data-level="normal" aria-pressed="true">
          <span class="difficulty-name">ふつう</span>
          <span class="difficulty-description">自然な口語・省略表現</span>
        </button>

        <button type="button" class="difficulty-card" data-level="hard" aria-pressed="false">
          <span class="difficulty-name">むずかしい</span>
          <span class="difficulty-description">ニュアンス重視の会話表現</span>
        </button>
      </div>

      <button id="start-button" type="button" class="button button-primary button-large">スタート</button>
    </section>

    <section id="countdown-screen" class="screen panel countdown-screen is-hidden" aria-live="assertive">
      <p>問題が出ます</p>
      <div id="countdown-number" class="countdown-number">3</div>
    </section>

    <section id="question-screen" class="screen panel is-hidden">
      <div class="question-meta">
        <div class="question-meta-left">
          <span id="difficulty-label" class="badge">ふつう</span>
          <span id="question-number">第1問</span>
        </div>
        <button id="finish-top-button" type="button" class="text-button danger-text">ゲームを終了</button>
      </div>

      <div class="question-card">
        <p>この英文を自然な日本語にしてください</p>
        <h2 id="english-question"></h2>
      </div>

      <div id="answer-area" class="answer-area">
        <label for="answer-input">あなたの和訳</label>
        <textarea id="answer-input" rows="4" placeholder="ここに日本語を入力してください"></textarea>
        <p id="input-message" class="input-message is-hidden" aria-live="polite"></p>
        <button id="submit-button" type="button" class="button button-primary button-large">送る</button>
      </div>

      <div id="feedback-area" class="feedback-area is-hidden" aria-live="polite">
        <div class="answer-review-card" aria-label="回答内容の比較">
          <section class="answer-review-section original-english-section">
            <p class="explanation-label">元の英文</p>
            <p id="review-english" class="review-english"></p>
          </section>

          <div class="answer-comparison-grid">
            <section class="answer-review-section user-answer-section">
              <p class="explanation-label">あなたの回答</p>
              <p id="review-user-answer" class="review-answer"></p>
            </section>

            <section class="answer-review-section correct-answer-section">
              <p class="explanation-label">模範解答</p>
              <p id="correct-answer" class="review-answer explanation-main"></p>
            </section>
          </div>
        </div>

        <div id="result-panel" class="result-panel">
          <p id="result-title" class="result-title"></p>
          <p id="result-comment" class="result-comment"></p>
        </div>

        <div class="feedback-card personal-feedback-card">
          <div class="card-heading-row">
            <div>
              <p class="explanation-label">あなたの文章に対するFB</p>
              <h3 class="feedback-heading">今回の回答をどう直すか</h3>
            </div>
            <span id="answer-score-badge" class="score-badge"></span>
          </div>
          <p id="personal-feedback" class="personal-feedback"></p>
          <div id="feedback-points" class="feedback-points"></div>
          <section class="suggested-rewrite-box">
            <p class="explanation-label">あなたの回答を直すなら</p>
            <p id="suggested-rewrite" class="suggested-rewrite"></p>
          </section>
        </div>

        <div class="explanation-card">
          <section>
            <p class="explanation-label">英文自体の解説</p>
            <p id="explanation"></p>
          </section>

          <section>
            <p class="explanation-label">実際の会話に近い読み方</p>
            <p id="pronunciation" class="pronunciation"></p>
          </section>
        </div>

        <div class="action-grid">
          <button id="next-button" type="button" class="button button-primary">次の問題</button>
          <button id="finish-button" type="button" class="button button-secondary">今日は終わる</button>
        </div>
      </div>
    </section>

    <section id="finish-screen" class="screen panel is-hidden">
      <div class="section-heading finish-heading">
        <span class="badge">GAME REPORT</span>
        <h2>今回の結果</h2>
        <p id="finish-level-label"></p>
      </div>

      <div class="result-grid result-grid-four">
        <div class="result-stat">
          <span>回答</span>
          <strong id="final-total">0</strong>
        </div>
        <div class="result-stat">
          <span>正解</span>
          <strong id="final-correct">0</strong>
        </div>
        <div class="result-stat">
          <span>だいたい</span>
          <strong id="final-almost">0</strong>
        </div>
        <div class="result-stat">
          <span>正答率</span>
          <strong id="final-rate">0%</strong>
        </div>
      </div>

      <section class="report-section report-highlight">
        <p class="explanation-label">総評</p>
        <h3 id="final-summary-title"></h3>
        <p id="final-message" class="final-message"></p>
      </section>

      <div class="report-grid">
        <section class="report-section">
          <p class="explanation-label">今回の傾向</p>
          <h3 id="final-tendency-title"></h3>
          <ul id="final-tendency-list" class="report-list"></ul>
        </section>

        <section class="report-section">
          <p class="explanation-label">フィードバック</p>
          <h3 id="final-feedback-title"></h3>
          <ul id="final-feedback-list" class="report-list"></ul>
        </section>
      </div>

      <section class="report-section next-action-section">
        <p class="explanation-label">ネクストアクション</p>
        <h3>次はここを意識してください</h3>
        <ol id="next-action-list" class="next-action-list"></ol>
      </section>

      <div class="finish-actions">
        <button id="restart-button" type="button" class="button button-primary">同じ難易度でもう一度</button>
        <button id="top-button" type="button" class="button button-secondary">TOPへ戻る</button>
      </div>
    </section>
  </main>

  <aside id="trend-toast" class="trend-toast is-hidden" aria-live="polite" aria-label="学習傾向">
    <div class="trend-toast-head">
      <div>
        <p id="trend-toast-kicker" class="trend-kicker">10問時点</p>
        <h2>あなたの傾向が見えてきました</h2>
      </div>
      <button id="trend-toast-close" type="button" class="toast-close" aria-label="傾向を閉じる">×</button>
    </div>
    <p id="trend-toast-summary"></p>
    <ul id="trend-toast-list"></ul>
  </aside>

  <script>
'use strict';

const questions = {
  easy: [
    {
      id: 'e01',
      en: 'I’ll be there in five minutes.',
      answer: 'あと5分で着くよ。',
      concepts: [
        { label: '5分後', category: 'time', keywords: ['5分', '五分'] },
        { label: '到着する', category: 'core', keywords: ['着く', '到着'] }
      ],
      explanation: '待ち合わせで、あとどのくらいで到着するかを伝える定番表現です。be there は文脈上「そこにいる」ではなく「そこへ着く」と訳すのが自然です。',
      reading: 'アイルビーゼァリン・ファイヴミニッツ',
      traps: [{ terms: ['そこにいる'], feedback: 'be there を直訳しています。この場面では「そこにいる」ではなく「着く」です。' }]
    },
    {
      id: 'e02',
      en: 'Take your time.',
      answer: 'ゆっくりで大丈夫だよ。',
      concepts: [
        { label: '急がなくてよい', category: 'consideration', keywords: ['ゆっくり', '急が', '焦ら'] },
        { label: '許容・気遣い', category: 'nuance', keywords: ['大丈夫', 'いいよ', '平気'] }
      ],
      explanation: '直訳ではなく「急がなくていいよ」という気遣いです。相手に時間を与える、柔らかい表現です。',
      reading: 'テイキュア・タイム',
      traps: [{ terms: ['時間を取って'], feedback: '単語は追えていますが、日本語では「時間を取って」とは言いません。「ゆっくりでいいよ」が自然です。' }]
    },
    {
      id: 'e03',
      en: 'I’m on my way.',
      answer: '今そっちに向かってるよ。',
      concepts: [
        { label: '移動中', category: 'aspect', keywords: ['向かって', '向かう', '移動中', '途中'] },
        { label: '現在', category: 'time', keywords: ['今', 'もう'] }
      ],
      explanation: 'すでに出発して、相手のいる場所へ移動している途中だと伝える表現です。',
      reading: 'アム・オンマイウェイ',
      traps: [{ terms: ['私の道'], feedback: 'on my way は「私の道の上」ではなく「向かっている途中」です。' }]
    },
    {
      id: 'e04',
      en: 'That works for me.',
      answer: '私はそれで大丈夫だよ。',
      concepts: [
        { label: 'その案でよい', category: 'agreement', keywords: ['それで', 'その案', 'その時間'] },
        { label: '都合が合う', category: 'nuance', keywords: ['大丈夫', '問題ない', '都合', 'いいよ'] }
      ],
      explanation: '日時や提案に対して「それで都合がいい」「その案で問題ない」と答える表現です。',
      reading: 'ザッ・ワークスファミー',
      traps: [{ terms: ['働く'], feedback: 'work を「働く」と取ると不自然です。ここでは「都合が合う・問題なく機能する」です。' }]
    },
    {
      id: 'e05',
      en: 'No worries. It happens.',
      answer: '気にしないで。そういうこともあるよ。',
      concepts: [
        { label: '気にしなくてよい', category: 'consideration', keywords: ['気にしない', '大丈夫', '心配しない'] },
        { label: 'よくあること', category: 'nuance', keywords: ['そういうことも', 'あるよ', 'よくある'] }
      ],
      explanation: '相手の謝罪に対して、責めずに受け流す表現です。It happens. は「それは起きる」より「そういうこともある」です。',
      reading: 'ノーウォーリーズ、イッハプンズ',
      traps: [{ terms: ['それは起きる'], feedback: 'It happens. の直訳感が強いです。「そういうこともあるよ」とすると会話になります。' }]
    },
    {
      id: 'e06',
      en: 'I’ll let you know.',
      answer: '分かったら連絡するね。',
      concepts: [
        { label: '後で知らせる', category: 'future', keywords: ['連絡', '知らせ', '伝え'] },
        { label: '判明後', category: 'time', keywords: ['分かったら', '決まったら', 'あとで'] }
      ],
      explanation: '情報が決まったり分かったりした後で、相手に知らせるという意味です。',
      reading: 'アイル・レッチュノウ',
      traps: [{ terms: ['あなたに知らせさせる'], feedback: 'let を使役で直訳しすぎています。まとまりで「知らせるね」です。' }]
    },
    {
      id: 'e07',
      en: 'I’m good, thanks.',
      answer: '大丈夫、ありがとう。',
      concepts: [
        { label: '断る・足りている', category: 'context', keywords: ['大丈夫', 'いらない', '結構'] },
        { label: '感謝', category: 'consideration', keywords: ['ありがとう', 'どうも'] }
      ],
      explanation: '何かを勧められた場面では「私は良い人です」ではなく、「大丈夫です・結構です」という断りです。',
      reading: 'アムグッ、センキュー',
      traps: [{ terms: ['私は良い'], feedback: 'good を性格評価として取っています。この場面では「もう大丈夫・結構」です。' }]
    },
    {
      id: 'e08',
      en: 'Sounds good.',
      answer: 'いいね。',
      concepts: [
        { label: '賛成・好印象', category: 'agreement', keywords: ['いいね', 'よさそう', 'いいと思う', '了解'] }
      ],
      explanation: '提案を聞いて「それいいね」「よさそう」と返す、とてもよく使う相づちです。',
      reading: 'サウンズグッ',
      traps: [{ terms: ['良く聞こえる'], feedback: '意味は近いですが、日本語の会話なら「いいね」で十分です。' }]
    },
    {
      id: 'e09',
      en: 'Give me a second.',
      answer: 'ちょっと待って。',
      concepts: [
        { label: '短く待つ', category: 'time', keywords: ['ちょっと待', '少し待', '一秒待'] }
      ],
      explanation: '本当に1秒という意味ではなく、「少し待って」という口語表現です。',
      reading: 'ギミアセカン',
      traps: [{ terms: ['一秒ください'], feedback: '直訳としては分かりますが、会話では「ちょっと待って」が自然です。' }]
    },
    {
      id: 'e10',
      en: 'I’m just looking.',
      answer: '見ているだけです。',
      concepts: [
        { label: '見るだけ', category: 'limitation', keywords: ['見てるだけ', '見ているだけ', '見るだけ'] }
      ],
      explanation: '店員に声をかけられたときなどに、「今は見ているだけです」と伝える表現です。',
      reading: 'アムジャス・ルッキン',
      traps: []
    },
    {
      id: 'e11',
      en: 'It’s up to you.',
      answer: 'あなたに任せるよ。',
      concepts: [
        { label: '相手に任せる', category: 'agency', keywords: ['任せる', 'あなた次第', 'そっちで決め'] }
      ],
      explanation: '決定権を相手に渡す表現です。「あなた次第だよ」「任せるよ」が自然です。',
      reading: 'イッツァップトゥユー',
      traps: [{ terms: ['あなたの上'], feedback: 'up to you は場所の話ではなく、「あなた次第・あなたに任せる」です。' }]
    },
    {
      id: 'e12',
      en: 'I didn’t catch that.',
      answer: '今の聞き取れなかった。',
      concepts: [
        { label: '聞き取れない', category: 'listening', keywords: ['聞き取れ', '聞こえな', '分からなかった'] },
        { label: '直前の発言', category: 'context', keywords: ['今の', 'それ'] }
      ],
      explanation: 'catch はここでは「捕まえる」ではなく、発言を聞き取ることです。',
      reading: 'アイディドゥン・キャッチザッ',
      traps: [{ terms: ['捕まえ'], feedback: 'catch の物理的な意味に引っ張られています。会話では「聞き取る」です。' }]
    }
  ],

  normal: [
    {
      id: 'n01',
      en: 'I’m running a little late, but you can start without me.',
      answer: '少し遅れるけど、先に始めてて大丈夫だよ。',
      concepts: [
        { label: '少し遅れる', category: 'time', keywords: ['少し遅れ', 'ちょっと遅れ', '遅刻'] },
        { label: '待たなくてよい', category: 'consideration', keywords: ['先に', '待たず', '私なし'] },
        { label: '開始してよい', category: 'permission', keywords: ['始めて', '開始して'] }
      ],
      explanation: 'run late は「遅れている」、without me は「私を待たずに」です。予定や食事の開始時によく使います。',
      reading: 'アム・ラニンナリトルレイッ、バッチュキャン・スターッウィダウッミー',
      traps: [{ terms: ['走って', '私なしで始めることができる'], feedback: '単語単位の直訳になっています。全体では「少し遅れるから、先に始めてて」です。' }]
    },
    {
      id: 'n02',
      en: 'I sent you a message. Haven’t you seen it yet?',
      answer: 'メッセージ送ったけど、まだ見てない？',
      concepts: [
        { label: '送信済み', category: 'aspect', keywords: ['送った', '送ってる'] },
        { label: 'まだ未確認', category: 'negative', keywords: ['まだ見てない', 'まだ見ていない', '見た？', '確認してない'] }
      ],
      explanation: 'Haven’t you ... yet? は「まだ〜してないの？」という確認です。言い方によっては少し責める響きも出ます。',
      reading: 'アイ・センチュアメセッジ、ハヴンチュ・スィーニッイェッ',
      traps: [{ terms: ['見ませんでしたか'], feedback: '文法上は追えていますが、日常会話では「まだ見てない？」のほうが自然です。' }]
    },
    {
      id: 'n03',
      en: 'I don’t want to get your hopes up, but I think I can do it.',
      answer: '期待させたくはないけど、たぶんできると思う。',
      concepts: [
        { label: '期待させたくない', category: 'consideration', keywords: ['期待させたく', 'ぬか喜びさせたく', '期待を持たせたく'] },
        { label: '可能性がある', category: 'possibility', keywords: ['できると思う', 'できそう', 'たぶんできる'] },
        { label: '断言を避ける', category: 'degree', keywords: ['たぶん', 'と思う', 'かも'] }
      ],
      explanation: 'get your hopes up は「期待を膨らませる」。断言を避けつつ、可能性はあると伝えます。',
      reading: 'アイドンワナ・ゲッチュアホウプスアップ、バライスィンク・アイキャンドゥイッ',
      traps: [{ terms: ['希望を上げ', 'ホープ'], feedback: 'get your hopes up を単語で処理しています。まとまりで「期待させる」です。' }]
    },
    {
      id: 'n04',
      en: 'Let’s just play it by ear.',
      answer: 'その場の流れで決めよう。',
      concepts: [
        { label: '状況を見る', category: 'idiom', keywords: ['その場', '流れ', '様子を見', '成り行き'] },
        { label: '柔軟に決める', category: 'agency', keywords: ['決めよう', '対応しよう', '臨機応変'] }
      ],
      explanation: 'play it by ear は、事前に細かく決めず、状況を見ながら対応するという意味です。',
      reading: 'レッツジャス・プレイリッバイイア',
      traps: [{ terms: ['耳', '演奏'], feedback: '慣用句を直訳しています。ここでは音楽ではなく「その場の流れで決める」です。' }]
    },
    {
      id: 'n05',
      en: 'I didn’t mean it like that.',
      answer: 'そういう意味で言ったんじゃない。',
      concepts: [
        { label: '意図の否定', category: 'negative', keywords: ['意味で言ったんじゃない', 'つもりじゃない', 'そういう意味じゃない'] },
        { label: '受け取り方の修正', category: 'intent', keywords: ['そういう', 'そんな'] }
      ],
      explanation: '自分の発言が違う意味に受け取られたとき、意図を訂正する表現です。',
      reading: 'アイディドゥン・ミーニッライクザッ',
      traps: [{ terms: ['そのように意味しなかった'], feedback: '意味は取れていますが、日本語として硬いです。「そういう意味じゃない」が会話的です。' }]
    },
    {
      id: 'n06',
      en: 'I’m not really in the mood to go out tonight.',
      answer: '今夜はあまり出かける気分じゃない。',
      concepts: [
        { label: '今夜', category: 'time', keywords: ['今夜', '今日の夜'] },
        { label: '出かける気分ではない', category: 'mood', keywords: ['出かける気分じゃない', '外出する気になれない', '出かけたくない'] },
        { label: '強すぎない否定', category: 'degree', keywords: ['あまり', 'そこまで', 'なんとなく'] }
      ],
      explanation: 'not really in the mood は「絶対嫌」ではなく、「あまりそういう気分ではない」という柔らかい断りです。',
      reading: 'アムナッ・リアリーインナムードゥ・トゥゴウアウッ・トゥナイッ',
      traps: [{ terms: ['ムードの中'], feedback: 'in the mood は場所ではなく「〜する気分」です。' }]
    },
    {
      id: 'n07',
      en: 'You might want to double-check that.',
      answer: 'それ、もう一度確認したほうがいいかも。',
      concepts: [
        { label: '再確認', category: 'action', keywords: ['もう一度確認', '再確認', '確認し直'] },
        { label: '柔らかい助言', category: 'consideration', keywords: ['ほうがいい', 'かも', 'した方が'] }
      ],
      explanation: 'might want to は直訳の「欲しいかもしれない」ではなく、押しつけを弱めた助言です。',
      reading: 'ユーマイッワナ・ダボーチェックザッ',
      traps: [{ terms: ['欲しいかもしれない'], feedback: 'might want to を欲求として直訳しています。ここでは「〜したほうがいいかも」です。' }]
    },
    {
      id: 'n08',
      en: 'I’ll see what I can do.',
      answer: 'できることがあるか確認してみるよ。',
      concepts: [
        { label: '対応を検討する', category: 'possibility', keywords: ['できること', '対応できるか', 'なんとかできるか'] },
        { label: '確認・試行', category: 'action', keywords: ['確認してみる', 'やってみる', '見てみる'] }
      ],
      explanation: '即答で約束せず、「できる範囲を確認してみる」と伝える表現です。',
      reading: 'アルスィー・ワライキャンドゥー',
      traps: [{ terms: ['何が見えるか'], feedback: 'see は視覚ではなく「確認する・考えてみる」です。' }]
    },
    {
      id: 'n09',
      en: 'It slipped my mind.',
      answer: 'うっかり忘れてた。',
      concepts: [
        { label: '忘れていた', category: 'core', keywords: ['忘れて', '忘れた'] },
        { label: '故意ではない', category: 'nuance', keywords: ['うっかり', '完全に', 'つい'] }
      ],
      explanation: '予定や用事をうっかり忘れたときの表現です。責任が消える魔法ではありませんが、言い方は柔らかくなります。',
      reading: 'イッ・スリップトマイマインド',
      traps: [{ terms: ['心から滑った', '頭から滑った'], feedback: 'イメージは近いですが、日本語では「うっかり忘れてた」です。' }]
    },
    {
      id: 'n10',
      en: 'I’m just giving you a heads-up.',
      answer: '一応、先に知らせておくね。',
      concepts: [
        { label: '事前に知らせる', category: 'time', keywords: ['先に知らせ', '事前に', '前もって'] },
        { label: '念のため', category: 'degree', keywords: ['一応', '念のため', 'とりあえず'] }
      ],
      explanation: 'heads-up は「事前の注意・予告」。問題が起きる前に軽く知らせる表現です。',
      reading: 'アムジャス・ギヴィンニュアヘッズアップ',
      traps: [{ terms: ['頭を上げ'], feedback: 'heads-up は身体動作ではなく、「事前に知らせること」です。' }]
    },
    {
      id: 'n11',
      en: 'I’m down for that.',
      answer: 'それ、いいよ。やろう。',
      concepts: [
        { label: '賛成', category: 'agreement', keywords: ['いいよ', '賛成', 'やろう', '参加する'] }
      ],
      explanation: 'カジュアルに「それやりたい」「参加する」と賛成する表現です。down を「落ち込む」と取らないのがポイントです。',
      reading: 'アムダウンフォーザッ',
      traps: [{ terms: ['落ち込ん', '下に'], feedback: 'down はここでは気分ではなく、「乗り気・参加する」です。' }]
    },
    {
      id: 'n12',
      en: 'I don’t blame you.',
      answer: 'そうなるのも無理ないよ。',
      concepts: [
        { label: '責めない', category: 'consideration', keywords: ['責めない', '悪くない'] },
        { label: '気持ちを理解する', category: 'empathy', keywords: ['無理ない', '分かる', '当然'] }
      ],
      explanation: '直訳は「あなたを責めない」ですが、会話では「そう思うのも無理ないよ」という共感になります。',
      reading: 'アイドン・ブレイミュー',
      traps: []
    },
    {
      id: 'n13',
      en: 'It’s not a big deal.',
      answer: '大したことじゃないよ。',
      concepts: [
        { label: '重大ではない', category: 'degree', keywords: ['大したことじゃない', '大きな問題じゃない', '気にしなくていい'] }
      ],
      explanation: '相手が気にしていることを「そこまで大きな問題ではない」と和らげる表現です。',
      reading: 'イッツナラ・ビッグディール',
      traps: [{ terms: ['大きな取引'], feedback: 'deal は取引ではなく、ここでは「重大なこと・問題」です。' }]
    },
    {
      id: 'n14',
      en: 'I could use a break.',
      answer: 'ちょっと休みたいな。',
      concepts: [
        { label: '休憩が必要', category: 'need', keywords: ['休みたい', '休憩したい', '休憩が必要'] },
        { label: '控えめな表現', category: 'degree', keywords: ['ちょっと', '少し', 'かな'] }
      ],
      explanation: 'could use は「使える」ではなく、「〜があると助かる・〜が必要」という控えめな言い方です。',
      reading: 'アイクッデューザ・ブレイク',
      traps: [{ terms: ['休憩を使える'], feedback: 'could use を能力として直訳しています。ここでは「休みたい・休憩が欲しい」です。' }]
    },
    {
      id: 'n15',
      en: 'That came out wrong.',
      answer: '今の言い方、誤解される言い方だった。',
      concepts: [
        { label: '言い方が悪かった', category: 'intent', keywords: ['言い方', '伝え方'] },
        { label: '意図と違って伝わった', category: 'nuance', keywords: ['誤解', '違って伝わ', '変に聞こえ'] }
      ],
      explanation: '発言内容そのものより、「口から出た言い方が意図と違って聞こえた」と訂正する表現です。',
      reading: 'ザッ・ケイムアウッロング',
      traps: [{ terms: ['間違って出てきた'], feedback: '構造の直訳になっています。「今の言い方はよくなかった」が自然です。' }]
    }
  ],

  hard: [
    {
      id: 'h01',
      en: 'I wouldn’t read too much into it.',
      answer: 'あまり深読みしないほうがいいと思う。',
      concepts: [
        { label: '深読み', category: 'idiom', keywords: ['深読み', '考えすぎ', '意味を持たせすぎ'] },
        { label: '控えめな助言', category: 'consideration', keywords: ['しないほうが', '考えないほうが', 'と思う'] }
      ],
      explanation: 'read too much into は、相手の言動に実際以上の意味を見いだすことです。恋愛相談で頻出ですが、深読み側だけが勝手に連続ドラマ化しがちです。',
      reading: 'アイ・ウドゥン・リードトゥーマッチ・イントゥイッ',
      traps: [{ terms: ['読みすぎ', '中に読む'], feedback: 'read into は読書ではなく、「裏の意味を読み取る・深読みする」です。' }]
    },
    {
      id: 'h02',
      en: 'It’s not that I don’t trust you. I just need some time.',
      answer: '信用してないわけじゃない。ただ少し時間が必要なの。',
      concepts: [
        { label: '不信ではない', category: 'negative', keywords: ['信用してないわけじゃない', '信じていないわけではない', '疑ってるわけじゃない'] },
        { label: '時間が必要', category: 'need', keywords: ['時間が必要', '少し時間', '時間がほしい'] }
      ],
      explanation: 'It’s not that ... は「〜というわけではない」。相手の解釈を否定してから、本当の事情を説明します。',
      reading: 'イッツナッダライ・ドン・トラスチュー、アイジャス・ニードサムタイム',
      traps: []
    },
    {
      id: 'h03',
      en: 'I was under the impression that we had already agreed on this.',
      answer: 'これはもう合意したものだと思っていました。',
      concepts: [
        { label: '合意済みの認識', category: 'aspect', keywords: ['合意した', '決めた', '話がついた', '決まった'] },
        { label: '自分の認識', category: 'perspective', keywords: ['と思っていました', '認識していました', 'つもりでした'] },
        { label: 'すでに', category: 'time', keywords: ['もう', 'すでに'] }
      ],
      explanation: 'be under the impression は「そう認識している」。丁寧ですが、認識違いを静かに指摘する表現です。',
      reading: 'アイワズ・アンダージインプレッション・ザッウィーハダレディ・アグリードンディス',
      traps: [{ terms: ['印象の下'], feedback: 'under the impression は位置関係ではなく、「〜だと認識している」です。' }]
    },
    {
      id: 'h04',
      en: 'I’m not trying to make excuses. I’m just telling you what happened.',
      answer: '言い訳をしているんじゃなくて、何があったか説明しているだけです。',
      concepts: [
        { label: '言い訳の否定', category: 'negative', keywords: ['言い訳をしているんじゃない', '言い訳するつもりじゃない', '言い訳ではない'] },
        { label: '事実の説明', category: 'intent', keywords: ['何があったか', '起きたこと', '事情'] },
        { label: '説明しているだけ', category: 'limitation', keywords: ['説明しているだけ', '伝えているだけ', '話しているだけ'] }
      ],
      explanation: '責任逃れと受け取られそうな場面で、自分の意図を明確にする表現です。',
      reading: 'アムナッ・トライナメイクイクスキューズィズ、アムジャス・テリンニュー・ワッハプンド',
      traps: []
    },
    {
      id: 'h05',
      en: 'I get where you’re coming from, but I don’t completely agree.',
      answer: '言いたいことは分かるけど、完全には同意できない。',
      concepts: [
        { label: '相手の立場を理解', category: 'empathy', keywords: ['言いたいことは分かる', '考えは分かる', '気持ちは分かる', '立場は理解'] },
        { label: '完全同意ではない', category: 'degree', keywords: ['完全には同意できない', '全部は賛成できない', '全面的には同意しない'] }
      ],
      explanation: '相手の立場は理解していると示しつつ、意見の違いを落ち着いて伝える表現です。',
      reading: 'アイゲッ・ウェアユアカミンフロム、バライドン・コンプリートリーアグリー',
      traps: [{ terms: ['どこから来た'], feedback: 'where you’re coming from は出身地ではなく、「その考えに至る立場・理由」です。' }]
    },
    {
      id: 'h06',
      en: 'I don’t want this to come across the wrong way.',
      answer: '変なふうに受け取ってほしくないんだけど。',
      concepts: [
        { label: '誤解されたくない', category: 'intent', keywords: ['変なふうに受け取', '誤解してほしくない', '悪く受け取'] },
        { label: '前置き', category: 'consideration', keywords: ['んだけど', 'けど', 'ですが'] }
      ],
      explanation: '少し言いにくいことを話す前に、「悪い意味に取らないでほしい」と予防線を張る表現です。',
      reading: 'アイドンワンディス・トゥカムアクロス・ザロングウェイ',
      traps: [{ terms: ['間違った道を渡る'], feedback: 'come across は移動ではなく、「相手に〜という印象で伝わる」です。' }]
    },
    {
      id: 'h07',
      en: 'I’m having second thoughts about it.',
      answer: 'やっぱり少し迷ってきた。',
      concepts: [
        { label: '考え直している', category: 'change', keywords: ['考え直', '迷って', '再検討'] },
        { label: '当初からの変化', category: 'aspect', keywords: ['やっぱり', 'してきた', '今になって'] }
      ],
      explanation: '一度決めたことに対して、あとから迷いや疑念が出てきた状態です。',
      reading: 'アムハヴィン・セカンドソーツ・アバウディッ',
      traps: [{ terms: ['二番目の考え'], feedback: 'second thoughts は順番ではなく、「考え直し・迷い」です。' }]
    },
    {
      id: 'h08',
      en: 'That’s beside the point.',
      answer: 'それは今の論点とは関係ない。',
      concepts: [
        { label: '論点外', category: 'logic', keywords: ['論点とは関係ない', '話がずれてる', '本題じゃない', '論点じゃない'] }
      ],
      explanation: '相手の発言が、本来議論しているポイントから外れていると指摘します。',
      reading: 'ザッツ・ビサイザポイント',
      traps: [{ terms: ['点の横'], feedback: 'beside the point は位置ではなく、「論点から外れている」です。' }]
    },
    {
      id: 'h09',
      en: 'I’m not ruling it out completely.',
      answer: '完全に可能性を否定しているわけではない。',
      concepts: [
        { label: '可能性を残す', category: 'possibility', keywords: ['可能性を否定しているわけではない', '選択肢から外してない', '可能性はある'] },
        { label: '完全否定ではない', category: 'negative', keywords: ['完全に', '全く', 'わけではない'] }
      ],
      explanation: '今すぐ賛成はしないものの、選択肢から完全には外していないという慎重な表現です。',
      reading: 'アムナッ・ルーリンギッアウッ・コンプリートリー',
      traps: [{ terms: ['支配', '規則'], feedback: 'rule out は規則ではなく、「可能性を除外する」です。' }]
    },
    {
      id: 'h10',
      en: 'I may have jumped to conclusions.',
      answer: '早とちりしたかもしれない。',
      concepts: [
        { label: '早とちり', category: 'logic', keywords: ['早とちり', '決めつけ', '結論を急い'] },
        { label: '可能性・反省', category: 'possibility', keywords: ['かもしれない', 'かも', '可能性がある'] }
      ],
      explanation: '十分な情報がないまま結論を出してしまった可能性を認める表現です。',
      reading: 'アイメイハヴ・ジャンプトゥコンクルージョンズ',
      traps: [{ terms: ['結論に飛んだ'], feedback: '英語の比喩をそのまま残しています。日本語では「早とちりした・決めつけた」です。' }]
    },
    {
      id: 'h11',
      en: 'I don’t think we’re on the same page.',
      answer: '私たち、認識が合ってないと思う。',
      concepts: [
        { label: '認識の不一致', category: 'perspective', keywords: ['認識が合ってない', '理解が一致してない', '話が噛み合ってない'] },
        { label: '控えめな指摘', category: 'consideration', keywords: ['と思う', '気がする'] }
      ],
      explanation: '同じ資料のページという意味ではなく、理解・前提・認識が揃っていないことを指します。',
      reading: 'アイドンスィンク・ウィアオンザセイムペイジ',
      traps: [{ terms: ['同じページ'], feedback: '比喩の直訳です。ここでは「認識が合っていない」です。' }]
    },
    {
      id: 'h12',
      en: 'That’s easier said than done.',
      answer: '言うのは簡単だけど、実際にやるのは難しい。',
      concepts: [
        { label: '言うのは簡単', category: 'contrast', keywords: ['言うのは簡単', '口で言うのは簡単'] },
        { label: '実行は難しい', category: 'contrast', keywords: ['やるのは難しい', '実行は難しい', '実際は難しい'] }
      ],
      explanation: '助言や理想論に対して、「言葉では簡単だが実行は難しい」と現実面を指摘します。',
      reading: 'ザッツイージア・セッザンダン',
      traps: []
    },
    {
      id: 'h13',
      en: 'I’m trying to wrap my head around it.',
      answer: 'それをなんとか理解しようとしてる。',
      concepts: [
        { label: '理解しようとしている', category: 'understanding', keywords: ['理解しよう', '把握しよう', '飲み込もう'] },
        { label: '難しさ', category: 'degree', keywords: ['なんとか', 'まだ', 'しようとして'] }
      ],
      explanation: '複雑な内容を頭の中で整理し、理解しようとしている状態です。',
      reading: 'アムトライナ・ラップマイヘッダラウンディッ',
      traps: [{ terms: ['頭を巻く'], feedback: 'wrap my head around は身体動作ではなく、「難しいことを理解する」です。' }]
    },
    {
      id: 'h14',
      en: 'I wouldn’t take it personally.',
      answer: '自分への悪意だとは受け取らないほうがいい。',
      concepts: [
        { label: '個人攻撃と思わない', category: 'perspective', keywords: ['自分への悪意', '個人攻撃', '自分のせい', '個人的に受け取'] },
        { label: '助言', category: 'consideration', keywords: ['受け取らないほうが', '気にしないほうが', '考えないほうが'] }
      ],
      explanation: '相手の態度を、自分個人への嫌悪や攻撃だと受け止めすぎないよう勧める表現です。',
      reading: 'アイウドゥン・テイキッパーソナリー',
      traps: [{ terms: ['個人的に取る'], feedback: '意味は近いですが、日本語としては「自分への悪意だと思わない」が自然です。' }]
    },
    {
      id: 'h15',
      en: 'It doesn’t sit right with me.',
      answer: 'どうも納得できない。',
      concepts: [
        { label: '違和感・不納得', category: 'mood', keywords: ['納得できない', '違和感', '腑に落ちない', '引っかかる'] },
        { label: '感覚的な抵抗', category: 'nuance', keywords: ['どうも', 'なんとなく', '少し'] }
      ],
      explanation: '論理的に完全否定するより、「どうも腑に落ちない・違和感がある」という感覚を表します。',
      reading: 'イッダズン・スィッライッウィズミー',
      traps: [{ terms: ['正しく座らない'], feedback: 'sit right は座り方ではなく、「しっくりくる・納得できる」です。' }]
    }
  ]
};

const categoryLabels = {
  action: '行動の把握', agency: '誰が決めるか', agreement: '賛否', aspect: '完了・進行', change: '気持ちの変化',
  consideration: '配慮・柔らかさ', context: '文脈判断', contrast: '対比', core: '中心意味', degree: '強さ・程度',
  empathy: '共感', future: '今後の動作', idiom: '慣用表現', intent: '発言意図', limitation: '「〜だけ」の限定',
  listening: '聞き取り表現', logic: '論理関係', mood: '気分・感情', need: '必要性', negative: '否定表現',
  nuance: 'ニュアンス', permission: '許可', perspective: '認識・視点', possibility: '可能性', time: '時間関係',
  understanding: '理解の表現'
};

const state = {
  level: 'normal',
  questionNumber: 0,
  current: null,
  queue: [],
  total: 0,
  correct: 0,
  almost: 0,
  wrong: 0,
  answered: false,
  records: [],
  categoryHits: {},
  categoryMisses: {},
  literalCount: 0,
  shortAnswerCount: 0,
  toastTimer: null
};

const screens = {
  start: document.getElementById('start-screen'),
  countdown: document.getElementById('countdown-screen'),
  question: document.getElementById('question-screen'),
  finish: document.getElementById('finish-screen')
};

const labels = { easy: 'かんたん', normal: 'ふつう', hard: 'むずかしい' };

function showScreen(name) {
  Object.entries(screens).forEach(([key, screen]) => screen.classList.toggle('is-hidden', key !== name));
}

function normalize(text) {
  return text
    .toLowerCase()
    .normalize('NFKC')
    .replace(/[\s　。、！？!?・「」『』（）()\-—…]/g, '')
    .replace(/です|ます|でした|だよ|だね|なの|だと思います/g, '');
}

function shuffle(items) {
  const result = [...items];
  for (let i = result.length - 1; i > 0; i -= 1) {
    const j = Math.floor(Math.random() * (i + 1));
    [result[i], result[j]] = [result[j], result[i]];
  }
  return result;
}

function bigrams(text) {
  const value = normalize(text);
  if (value.length < 2) return value ? [value] : [];
  const grams = [];
  for (let i = 0; i < value.length - 1; i += 1) grams.push(value.slice(i, i + 2));
  return grams;
}

function diceSimilarity(a, b) {
  const gramsA = bigrams(a);
  const gramsB = bigrams(b);
  if (!gramsA.length || !gramsB.length) return 0;
  const counts = new Map();
  gramsA.forEach((gram) => counts.set(gram, (counts.get(gram) || 0) + 1));
  let overlap = 0;
  gramsB.forEach((gram) => {
    const count = counts.get(gram) || 0;
    if (count > 0) {
      overlap += 1;
      counts.set(gram, count - 1);
    }
  });
  return (2 * overlap) / (gramsA.length + gramsB.length);
}

function refillQueue() {
  state.queue = shuffle(questions[state.level]);
  if (state.current && state.queue.length > 1 && state.queue[0].id === state.current.id) {
    [state.queue[0], state.queue[1]] = [state.queue[1], state.queue[0]];
  }
}

function chooseQuestion() {
  if (!state.queue.length) refillQueue();
  state.current = state.queue.shift();
}

function updateHeader() {
  document.getElementById('header-total').textContent = String(state.total);
  document.getElementById('header-score').textContent = String(state.correct);
  document.getElementById('header-stats').classList.toggle('is-hidden', screens.start.classList.contains('is-hidden') === false);
}

function runCountdown() {
  document.getElementById('header-stats').classList.add('is-hidden');
  showScreen('countdown');
  const number = document.getElementById('countdown-number');
  let count = 3;
  number.textContent = String(count);

  const timer = window.setInterval(() => {
    count -= 1;
    if (count === 0) {
      window.clearInterval(timer);
      window.setTimeout(showQuestion, 220);
      return;
    }
    number.style.animation = 'none';
    void number.offsetWidth;
    number.textContent = String(count);
    number.style.animation = '';
  }, 800);
}

function showQuestion() {
  chooseQuestion();
  state.questionNumber += 1;
  state.answered = false;

  document.getElementById('difficulty-label').textContent = labels[state.level];
  document.getElementById('question-number').textContent = `第${state.questionNumber}問`;
  document.getElementById('english-question').textContent = state.current.en;

  const answerInput = document.getElementById('answer-input');
  const submitButton = document.getElementById('submit-button');
  answerInput.value = '';
  answerInput.disabled = false;
  submitButton.disabled = false;

  document.getElementById('feedback-area').classList.add('is-hidden');
  document.getElementById('input-message').classList.add('is-hidden');
  document.getElementById('header-stats').classList.remove('is-hidden');
  updateHeader();
  showScreen('question');
  window.scrollTo({ top: 0, behavior: 'smooth' });
  window.setTimeout(() => answerInput.focus(), 50);
}

function gradeAnswer(answer) {
  const normalized = normalize(answer);
  const matchedConcepts = [];
  const missingConcepts = [];

  state.current.concepts.forEach((concept) => {
    const hit = concept.keywords.some((keyword) => normalized.includes(normalize(keyword)));
    (hit ? matchedConcepts : missingConcepts).push(concept);
  });

  const conceptRatio = matchedConcepts.length / state.current.concepts.length;
  const similarity = diceSimilarity(answer, state.current.answer);
  const score = Math.max(conceptRatio, similarity * 0.9);
  const trap = (state.current.traps || []).find((item) => item.terms.some((term) => normalized.includes(normalize(term))));

  let result = 'wrong';
  if (score >= 0.78 && !trap) result = 'correct';
  else if (score >= 0.43 || (conceptRatio >= 0.5 && trap)) result = 'almost';

  return {
    result,
    score: Math.round(score * 100),
    conceptRatio,
    similarity,
    matchedConcepts,
    missingConcepts,
    trap,
    isShort: normalize(answer).length <= 5
  };
}

function buildPersonalFeedback(answer, analysis) {
  const missingNames = analysis.missingConcepts.map((item) => `「${item.label}」`);
  const matchedNames = analysis.matchedConcepts.map((item) => `「${item.label}」`);
  let main;
  let suggestedRewrite = state.current.answer;

  if (analysis.result === 'correct') {
    main = `「${answer}」は、元の英文が伝えている内容を自然な日本語として成立させています。`;
    if (analysis.similarity < 0.45) {
      main += ' 模範解答とは言葉選びが違いますが、意味のズレではなく表現の違いです。';
    } else {
      main += ' 模範解答との違いも小さく、そのまま会話で使える水準です。';
    }
    suggestedRewrite = answer.replace(/[。！？!?]+$/, '') + (/[？?]$/.test(state.current.answer) ? '？' : '。');
  } else if (analysis.result === 'almost') {
    main = `「${answer}」でも中心の意味は伝わります。`;
    if (matchedNames.length) main += ` ${matchedNames.join('・')}は拾えています。`;
    if (missingNames.length) main += ` 一方で、${missingNames.join('・')}が文面に出ていないため、英文より情報が少なくなっています。`;
  } else {
    main = `「${answer}」は、元の英文と比べると伝わる内容がずれています。`;
    if (matchedNames.length) main += ` ${matchedNames.join('・')}までは拾えていますが、`;
    if (missingNames.length) main += `${missingNames.join('・')}が抜けているため、英文の中心まで届いていません。`;
  }

  const points = [];
  if (matchedNames.length) {
    points.push({
      type: 'good',
      title: '拾えている部分',
      text: `${matchedNames.join('・')}は、あなたの回答にも入っています。ここは残して大丈夫です。`
    });
  }

  if (analysis.trap) {
    points.push({ type: 'fix', title: 'ズレた部分', text: analysis.trap.feedback });
  } else if (missingNames.length) {
    points.push({
      type: 'fix',
      title: '足りない部分',
      text: `${missingNames.join('・')}を加えると、元の英文が持つ情報量に近づきます。`
    });
  }

  if (analysis.isShort && analysis.result !== 'correct') {
    points.push({
      type: 'fix',
      title: '文章の作り方',
      text: '回答を短くまとめたことで、意味の一部が落ちています。送る前に「否定・時間・程度・相手への配慮」が残っているか確認してください。'
    });
  } else if (analysis.result === 'correct') {
    points.push({
      type: 'good',
      title: '日本語の自然さ',
      text: '英単語を順番に置き換えず、日本語の会話として組み直せています。'
    });
  } else {
    points.push({
      type: 'fix',
      title: '直し方',
      text: `あなたの回答の言いたい方向は残しつつ、最終的には「${state.current.answer}」の情報が揃う形に直してください。`
    });
  }

  return { main, points, suggestedRewrite };
}

function addCategoryStats(analysis) {
  analysis.matchedConcepts.forEach((concept) => {
    state.categoryHits[concept.category] = (state.categoryHits[concept.category] || 0) + 1;
  });
  analysis.missingConcepts.forEach((concept) => {
    state.categoryMisses[concept.category] = (state.categoryMisses[concept.category] || 0) + 1;
  });
  if (analysis.trap) state.literalCount += 1;
  if (analysis.isShort && analysis.result !== 'correct') state.shortAnswerCount += 1;
}

function displayFeedback(answer, analysis) {
  const panel = document.getElementById('result-panel');
  const title = document.getElementById('result-title');
  const comment = document.getElementById('result-comment');
  panel.classList.remove('is-correct', 'is-almost', 'is-wrong');

  if (analysis.result === 'correct') {
    panel.classList.add('is-correct');
    title.textContent = '正解！';
    comment.textContent = '意味もニュアンスも取れています。';
    state.correct += 1;
  } else if (analysis.result === 'almost') {
    panel.classList.add('is-almost');
    title.textContent = 'だいたい大丈夫';
    comment.textContent = '大筋は合っています。抜けた要素を確認しましょう。';
    state.almost += 1;
  } else {
    panel.classList.add('is-wrong');
    title.textContent = '間違い';
    comment.textContent = '今回は意味がずれています。ここで事故原因を潰します。';
    state.wrong += 1;
  }

  state.total += 1;
  state.answered = true;
  addCategoryStats(analysis);

  const personal = buildPersonalFeedback(answer, analysis);
  state.records.push({
    question: state.current.en,
    answer,
    result: analysis.result,
    score: analysis.score,
    matched: analysis.matchedConcepts.map((item) => item.label),
    missing: analysis.missingConcepts.map((item) => item.label),
    trap: analysis.trap ? analysis.trap.feedback : '',
    categoriesMissed: analysis.missingConcepts.map((item) => item.category)
  });

  document.getElementById('review-english').textContent = state.current.en;
  document.getElementById('review-user-answer').textContent = answer;
  document.getElementById('answer-score-badge').textContent = `一致度 ${analysis.score}%`;
  document.getElementById('personal-feedback').textContent = personal.main;
  document.getElementById('suggested-rewrite').textContent = personal.suggestedRewrite;

  const pointsContainer = document.getElementById('feedback-points');
  pointsContainer.replaceChildren();
  personal.points.forEach((point) => {
    const row = document.createElement('div');
    row.className = `feedback-point is-${point.type}`;
    const strong = document.createElement('strong');
    strong.textContent = point.title;
    const text = document.createElement('span');
    text.textContent = point.text;
    row.append(strong, text);
    pointsContainer.appendChild(row);
  });

  document.getElementById('correct-answer').textContent = state.current.answer;
  document.getElementById('explanation').textContent = state.current.explanation;
  document.getElementById('pronunciation').textContent = state.current.reading;
  document.getElementById('feedback-area').classList.remove('is-hidden');
  document.getElementById('answer-input').disabled = true;
  document.getElementById('submit-button').disabled = true;
  updateHeader();

  if (state.total % 10 === 0) showTrendToast();
  window.setTimeout(() => document.getElementById('result-panel').scrollIntoView({ behavior: 'smooth', block: 'start' }), 80);
}

function submitAnswer() {
  if (state.answered) return;
  const input = document.getElementById('answer-input');
  const answer = input.value.trim();
  const inputMessage = document.getElementById('input-message');

  if (!answer) {
    inputMessage.textContent = '和訳を入力してください。無回答は潔いですが、採点はできません。';
    inputMessage.classList.remove('is-hidden');
    input.focus();
    return;
  }

  inputMessage.classList.add('is-hidden');
  displayFeedback(answer, gradeAnswer(answer));
}

function sortedCategoryEntries(source) {
  return Object.entries(source).sort((a, b) => b[1] - a[1]);
}

function buildTrend() {
  const misses = sortedCategoryEntries(state.categoryMisses);
  const hits = sortedCategoryEntries(state.categoryHits);
  const weakest = misses[0] ? categoryLabels[misses[0][0]] : '大きな弱点なし';
  const strongest = hits[0] ? categoryLabels[hits[0][0]] : '分析中';
  const rate = state.total ? Math.round((state.correct / state.total) * 100) : 0;
  const points = [];

  if (misses[0]) points.push(`最も落としやすいのは「${weakest}」です。`);
  if (hits[0]) points.push(`一方で「${strongest}」は安定しています。`);
  if (state.literalCount >= Math.max(2, Math.ceil(state.total * 0.2))) {
    points.push(`直訳に引っ張られた回答が${state.literalCount}回あります。語句ではなく文全体で意味を取るのが次の課題です。`);
  } else {
    points.push('直訳への引っ張られ方は強くありません。日本語として組み直す意識があります。');
  }
  if (state.shortAnswerCount >= 2) points.push(`情報を省きすぎた回答が${state.shortAnswerCount}回あります。否定・程度・時間を最後に確認してください。`);

  return {
    rate,
    weakest,
    strongest,
    summary: rate >= 80
      ? 'かなり安定しています。細かなニュアンスを詰める段階です。'
      : rate >= 50
        ? '意味の中心は取れていますが、特定の要素が落ちる傾向があります。'
        : '単語は拾えていますが、文全体の意味へまとめる部分で崩れています。',
    points
  };
}

function showTrendToast() {
  const trend = buildTrend();
  const toast = document.getElementById('trend-toast');
  document.getElementById('trend-toast-kicker').textContent = `${state.total}問時点`;
  document.getElementById('trend-toast-summary').textContent = trend.summary;
  const list = document.getElementById('trend-toast-list');
  list.replaceChildren();
  trend.points.slice(0, 3).forEach((point) => {
    const li = document.createElement('li');
    li.textContent = point;
    list.appendChild(li);
  });
  toast.classList.remove('is-hidden');
  window.clearTimeout(state.toastTimer);
  state.toastTimer = window.setTimeout(() => toast.classList.add('is-hidden'), 15000);
}

function appendListItems(elementId, items) {
  const list = document.getElementById(elementId);
  list.replaceChildren();
  items.forEach((item) => {
    const li = document.createElement('li');
    li.textContent = item;
    list.appendChild(li);
  });
}

function buildFinalReport() {
  const trend = buildTrend();
  const rate = trend.rate;
  const recentMisses = state.records.flatMap((record) => record.missing).filter(Boolean);
  const missedCounts = recentMisses.reduce((acc, item) => {
    acc[item] = (acc[item] || 0) + 1;
    return acc;
  }, {});
  const frequentMisses = Object.entries(missedCounts).sort((a, b) => b[1] - a[1]).slice(0, 3).map(([label]) => label);

  let summaryTitle = 'まずは英文の中心を一本にまとめる段階です';
  let message = '単語を個別に訳した後、それらを一文の意味としてまとめ切れない場面があります。英文を前から追いながら、「結局この人は何を伝えたいのか」を先に決めてください。';
  if (rate >= 80) {
    summaryTitle = '会話としてかなり成立しています';
    message = '主要な意味は安定して取れています。今後は、否定の強さや遠回しさなど、正解・不正解の間にある細かなニュアンスを詰める段階です。';
  } else if (rate >= 50) {
    summaryTitle = '意味は取れています。抜け方に癖があります';
    message = '全体像は理解できていますが、否定・程度・時間・配慮などの補助情報が落ちると「だいたい大丈夫」に留まります。最後の一確認で正解へ上げられます。';
  }

  const tendencyItems = [...trend.points];
  if (!state.total) tendencyItems.splice(0, tendencyItems.length, 'まだ回答データがないため、傾向は判定できません。');

  const feedbackItems = [];
  if (frequentMisses.length) feedbackItems.push(`今回よく抜けた要素：${frequentMisses.map((item) => `「${item}」`).join('・')}。`);
  if (state.literalCount) feedbackItems.push(`慣用句や口語を直訳した回答が${state.literalCount}回ありました。単語の辞書的意味より、会話の目的を優先してください。`);
  if (state.shortAnswerCount) feedbackItems.push(`短くまとめすぎて情報が欠けた回答が${state.shortAnswerCount}回ありました。短さより、意味の骨格を残すことが先です。`);
  if (!feedbackItems.length && state.total) feedbackItems.push('大きな直訳癖や情報不足は目立ちませんでした。自然な日本語への言い換えができています。');
  if (!state.total) feedbackItems.push('1問以上回答すると、入力内容に基づくフィードバックが表示されます。');

  const weakCategory = trend.weakest;
  const nextActions = state.total ? [
    `次の10問は「${weakCategory}」を意識し、送信前にその要素が訳へ入っているか確認する。`,
    '模範訳とカタカナ読みを1回ずつ声に出し、英語を意味の塊で読む。単語ごとのカタカナ読みには戻さない。',
    state.literalCount
      ? '慣用句が出たら直訳を一度疑い、「日本人ならこの場面で何と言うか」に置き換える。'
      : '正解した問題も、別の自然な日本語で言い換えられるか1案だけ考える。'
  ] : ['まず1問回答し、回答後の個別フィードバックを確認する。'];

  return { trend, summaryTitle, message, tendencyItems, feedbackItems, nextActions };
}

function finishGame() {
  window.clearTimeout(state.toastTimer);
  document.getElementById('trend-toast').classList.add('is-hidden');
  const report = buildFinalReport();

  document.getElementById('final-total').textContent = String(state.total);
  document.getElementById('final-correct').textContent = String(state.correct);
  document.getElementById('final-almost').textContent = String(state.almost);
  document.getElementById('final-rate').textContent = `${report.trend.rate}%`;
  document.getElementById('finish-level-label').textContent = `${labels[state.level]}レベル・${state.total}問回答`;
  document.getElementById('final-summary-title').textContent = report.summaryTitle;
  document.getElementById('final-message').textContent = report.message;
  document.getElementById('final-tendency-title').textContent = state.total ? `強みは「${report.trend.strongest}」、課題は「${report.trend.weakest}」` : '回答後に傾向を分析します';
  document.getElementById('final-feedback-title').textContent = state.total ? '回答の崩れ方を整理しました' : 'まだ分析データがありません';
  appendListItems('final-tendency-list', report.tendencyItems);
  appendListItems('final-feedback-list', report.feedbackItems);
  appendListItems('next-action-list', report.nextActions);

  document.getElementById('header-stats').classList.add('is-hidden');
  showScreen('finish');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function resetSession({ keepLevel = true } = {}) {
  const selectedLevel = keepLevel ? state.level : 'normal';
  Object.assign(state, {
    level: selectedLevel,
    questionNumber: 0,
    current: null,
    queue: [],
    total: 0,
    correct: 0,
    almost: 0,
    wrong: 0,
    answered: false,
    records: [],
    categoryHits: {},
    categoryMisses: {},
    literalCount: 0,
    shortAnswerCount: 0,
    toastTimer: null
  });
  document.getElementById('header-total').textContent = '0';
  document.getElementById('header-score').textContent = '0';
  document.getElementById('trend-toast').classList.add('is-hidden');
}

function goTop() {
  resetSession({ keepLevel: false });
  document.querySelectorAll('.difficulty-card').forEach((button) => {
    const selected = button.dataset.level === 'normal';
    button.classList.toggle('is-selected', selected);
    button.setAttribute('aria-pressed', String(selected));
  });
  document.getElementById('header-stats').classList.add('is-hidden');
  showScreen('start');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

document.querySelectorAll('.difficulty-card').forEach((button) => {
  button.addEventListener('click', () => {
    state.level = button.dataset.level;
    document.querySelectorAll('.difficulty-card').forEach((item) => {
      const selected = item === button;
      item.classList.toggle('is-selected', selected);
      item.setAttribute('aria-pressed', String(selected));
    });
  });
});

document.getElementById('start-button').addEventListener('click', () => {
  resetSession({ keepLevel: true });
  runCountdown();
});
document.getElementById('submit-button').addEventListener('click', submitAnswer);
document.getElementById('next-button').addEventListener('click', showQuestion);
document.getElementById('finish-button').addEventListener('click', finishGame);
document.getElementById('finish-top-button').addEventListener('click', finishGame);
document.getElementById('restart-button').addEventListener('click', () => {
  resetSession({ keepLevel: true });
  runCountdown();
});
document.getElementById('top-button').addEventListener('click', goTop);
document.getElementById('trend-toast-close').addEventListener('click', () => {
  window.clearTimeout(state.toastTimer);
  document.getElementById('trend-toast').classList.add('is-hidden');
});

document.getElementById('answer-input').addEventListener('keydown', (event) => {
  if ((event.metaKey || event.ctrlKey) && event.key === 'Enter') submitAnswer();
});

</script>
</body>
</html>
