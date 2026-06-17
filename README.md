<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>역사 탐험대 퀴즈 · 1~3학년</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    font-family: "Apple SD Gothic Neo", "Noto Sans KR", sans-serif;
    background: #F0F7E8;
    min-height: 100vh;
    display: flex;
    align-items: flex-start;
    justify-content: center;
    padding: 24px 16px 48px;
  }
  .container { width: 100%; max-width: 520px; }

  /* 헤더 */
  .header {
    background: #3B6D11;
    border-radius: 18px;
    padding: 24px 20px;
    text-align: center;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .header-text { flex: 1; }
  .header .tag {
    display: inline-block;
    background: #FAC775;
    color: #633806;
    font-size: 13px;
    font-weight: 800;
    padding: 3px 14px;
    border-radius: 20px;
    margin-bottom: 8px;
  }
  .header h1 { color: #fff; font-size: 22px; font-weight: 900; line-height: 1.25; }
  .header .sub { color: #C0DD97; font-size: 13px; font-weight: 700; margin-top: 4px; }

  /* 진행 바 */
  .progress-wrap { margin-bottom: 20px; }
  .progress-bar-bg { height: 8px; background: #C0DD97; border-radius: 4px; margin-bottom: 6px; }
  .progress-bar-fill { height: 8px; background: #3B6D11; border-radius: 4px; transition: width 0.4s; }
  .progress-label { font-size: 13px; color: #639922; font-weight: 700; text-align: right; }

  /* 문제 카드 */
  .q-card {
    background: #fff;
    border: 2px solid #C0DD97;
    border-radius: 18px;
    padding: 22px 20px;
    margin-bottom: 14px;
  }
  .q-badge {
    display: inline-block;
    font-size: 12px;
    font-weight: 800;
    padding: 3px 12px;
    border-radius: 20px;
    margin-bottom: 12px;
  }
  .badge-ox { background: #EAF3DE; color: #3B6D11; }
  .badge-choice { background: #E6F1FB; color: #185FA5; }
  .q-text {
    font-size: 18px;
    font-weight: 800;
    color: #173404;
    line-height: 1.55;
    margin-bottom: 18px;
  }
  .q-illust {
    background: #F0F7E8;
    border-radius: 12px;
    padding: 14px;
    text-align: center;
    margin-bottom: 18px;
  }
  .q-illust svg { display: block; margin: 0 auto; }
  .illust-cap { font-size: 12px; color: #639922; margin-top: 6px; font-weight: 600; }

  /* OX 버튼 */
  .ox-row { display: flex; gap: 12px; }
  .ox-btn {
    flex: 1;
    height: 80px;
    border: 2.5px solid #C0DD97;
    border-radius: 16px;
    background: #fff;
    cursor: pointer;
    font-size: 36px;
    font-weight: 900;
    color: #2C2C2A;
    transition: all 0.15s;
  }
  .ox-btn:hover:not(:disabled) { background: #EAF3DE; }
  .ox-btn.correct { border-color: #3B6D11; background: #EAF3DE; color: #27500A; }
  .ox-btn.wrong   { border-color: #A32D2D; background: #FCEBEB; color: #791F1F; opacity: 0.55; }

  /* 선택지 */
  .choice-list { display: flex; flex-direction: column; gap: 10px; }
  .choice-btn {
    width: 100%;
    text-align: left;
    padding: 14px 16px;
    border: 2.5px solid #C0DD97;
    border-radius: 14px;
    background: #fff;
    cursor: pointer;
    font-size: 16px;
    font-weight: 700;
    color: #2C2C2A;
    display: flex;
    align-items: center;
    gap: 12px;
    transition: all 0.15s;
  }
  .choice-btn:hover:not(:disabled) { background: #EAF3DE; }
  .choice-btn .num {
    width: 28px; height: 28px;
    border-radius: 50%;
    background: #EAF3DE;
    color: #3B6D11;
    font-size: 13px;
    font-weight: 900;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }
  .choice-btn.correct { border-color: #3B6D11; background: #EAF3DE; color: #27500A; }
  .choice-btn.correct .num { background: #3B6D11; color: #fff; }
  .choice-btn.wrong { border-color: #A32D2D; background: #FCEBEB; color: #791F1F; opacity: 0.55; }
  .choice-btn.wrong .num { background: #A32D2D; color: #fff; }

  /* 피드백 */
  .feedback {
    margin-top: 14px;
    padding: 14px 16px;
    border-radius: 12px;
    font-size: 15px;
    font-weight: 700;
    line-height: 1.6;
    display: none;
  }
  .feedback.correct { background: #EAF3DE; color: #27500A; }
  .feedback.wrong   { background: #FCEBEB; color: #791F1F; }

  /* 다음 버튼 */
  .next-btn {
    display: none;
    width: 100%;
    padding: 16px;
    background: #3B6D11;
    color: #fff;
    border: none;
    border-radius: 14px;
    font-size: 17px;
    font-weight: 900;
    cursor: pointer;
    margin-top: 12px;
    transition: background 0.15s;
  }
  .next-btn:hover { background: #27500A; }

  /* 결과 화면 */
  .result-card {
    background: #fff;
    border: 2px solid #C0DD97;
    border-radius: 18px;
    padding: 32px 24px;
    text-align: center;
    display: none;
  }
  .result-soldier { margin-bottom: 12px; }
  .result-stars { font-size: 34px; letter-spacing: 5px; margin-bottom: 10px; }
  .result-score { font-size: 54px; font-weight: 900; color: #3B6D11; line-height: 1; margin-bottom: 4px; }
  .result-total { font-size: 15px; color: #639922; margin-bottom: 16px; }
  .result-msg { font-size: 19px; font-weight: 800; color: #173404; margin-bottom: 24px; line-height: 1.5; white-space: pre-line; }
  .retry-btn {
    padding: 14px 36px;
    border: 2.5px solid #C0DD97;
    border-radius: 14px;
    background: #EAF3DE;
    color: #27500A;
    font-size: 16px;
    font-weight: 800;
    cursor: pointer;
    transition: background 0.15s;
  }
  .retry-btn:hover { background: #C0DD97; }
</style>
</head>
<body>
<div class="container">

  <div class="header">
    <svg width="70" height="82" viewBox="0 0 84 100" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
      <ellipse cx="42" cy="95" rx="26" ry="4" fill="#27500A"/>
      <rect x="28" y="58" width="28" height="28" rx="8" fill="#639922"/>
      <rect x="28" y="58" width="28" height="9" fill="#3B6D11"/>
      <rect x="24" y="80" width="11" height="16" rx="4" fill="#444441"/>
      <rect x="49" y="80" width="11" height="16" rx="4" fill="#444441"/>
      <rect x="20" y="60" width="9" height="20" rx="4.5" fill="#639922"/>
      <path d="M55 62 Q66 56 64 44" stroke="#639922" stroke-width="9" stroke-linecap="round" fill="none"/>
      <circle cx="64" cy="42" r="4.5" fill="#F5C4B3"/>
      <circle cx="42" cy="38" r="19" fill="#FBE3D4"/>
      <path d="M22 34 Q22 16 42 16 Q62 16 62 34 L62 36 Q42 30 22 36 Z" fill="#3B6D11"/>
      <rect x="20" y="33" width="44" height="6" rx="3" fill="#27500A"/>
      <circle cx="42" cy="24" r="3.5" fill="#FAC775"/>
      <circle cx="35" cy="42" r="2.4" fill="#2C2C2A"/>
      <circle cx="49" cy="42" r="2.4" fill="#2C2C2A"/>
      <circle cx="36" cy="41" r="0.8" fill="#fff"/>
      <circle cx="50" cy="41" r="0.8" fill="#fff"/>
      <circle cx="30" cy="47" r="2.5" fill="#F5C4B3" opacity="0.7"/>
      <circle cx="54" cy="47" r="2.5" fill="#F5C4B3" opacity="0.7"/>
      <path d="M38 49 Q42 52 46 49" stroke="#2C2C2A" stroke-width="1.6" stroke-linecap="round" fill="none"/>
    </svg>
    <div class="header-text">
      <div class="tag">1~3학년 · 역사 탐험대</div>
      <h1>나라를 지킨<br>사람들 퀴즈</h1>
      <div class="sub">책자를 잘 읽었으면 모두 맞출 수 있어요!</div>
    </div>
  </div>

  <div id="quiz-section">
    <div class="progress-wrap">
      <div class="progress-bar-bg"><div class="progress-bar-fill" id="prog"></div></div>
      <div class="progress-label" id="prog-label"></div>
    </div>
    <div class="q-card" id="q-card"></div>
    <button class="next-btn" id="next-btn"></button>
  </div>

  <div class="result-card" id="result-card">
    <div class="result-soldier">
      <svg width="72" height="85" viewBox="0 0 84 100" xmlns="http://www.w3.org/2000/svg" aria-hidden="true">
        <ellipse cx="42" cy="95" rx="26" ry="4" fill="#27500A"/>
        <rect x="28" y="58" width="28" height="28" rx="8" fill="#639922"/>
        <rect x="28" y="58" width="28" height="9" fill="#3B6D11"/>
        <rect x="24" y="80" width="11" height="16" rx="4" fill="#444441"/>
        <rect x="49" y="80" width="11" height="16" rx="4" fill="#444441"/>
        <rect x="55" y="60" width="9" height="20" rx="4.5" fill="#639922"/>
        <rect x="14" y="62" width="9" height="14" rx="4.5" fill="#639922"/>
        <rect x="16.5" y="28" width="3" height="38" rx="1.5" fill="#854F0B"/>
        <rect x="19.5" y="28" width="24" height="16" rx="2" fill="#fff" stroke="#D3D1C7" stroke-width="0.8"/>
        <circle cx="31.5" cy="36" r="4.5" fill="#E24B4A"/>
        <path d="M27 36 A4.5 4.5 0 0 1 36 36 A2.25 2.25 0 0 1 31.5 36 A2.25 2.25 0 0 0 27 36 Z" fill="#185FA5"/>
        <circle cx="42" cy="38" r="19" fill="#FBE3D4"/>
        <path d="M22 34 Q22 16 42 16 Q62 16 62 34 L62 36 Q42 30 22 36 Z" fill="#3B6D11"/>
        <rect x="20" y="33" width="44" height="6" rx="3" fill="#27500A"/>
        <circle cx="42" cy="24" r="3.5" fill="#FAC775"/>
        <circle cx="35" cy="42" r="2.4" fill="#2C2C2A"/>
        <circle cx="49" cy="42" r="2.4" fill="#2C2C2A"/>
        <circle cx="36" cy="41" r="0.8" fill="#fff"/>
        <circle cx="50" cy="41" r="0.8" fill="#fff"/>
        <circle cx="30" cy="47" r="2.5" fill="#F5C4B3" opacity="0.7"/>
        <circle cx="54" cy="47" r="2.5" fill="#F5C4B3" opacity="0.7"/>
        <path d="M37 48 Q42 53 47 48" stroke="#2C2C2A" stroke-width="1.6" stroke-linecap="round" fill="none"/>
      </svg>
    </div>
    <div class="result-stars" id="result-stars"></div>
    <div class="result-score" id="result-score"></div>
    <div class="result-total">5문제 중</div>
    <div class="result-msg" id="result-msg"></div>
    <button class="retry-btn" onclick="startQuiz()">다시 도전하기</button>
  </div>

</div>

<script>
const questions = [
  {
    type: "ox",
    text: "현충일은 매년 6월 6일이에요.",
    illust: null,
    answer: "O",
    ok: "맞아요! 현충일은 매년 6월 6일이에요.\n나라를 위해 싸우다 돌아가신 분들을 기억하는 날이에요.",
    no: "아쉬워요! 현충일은 6월 6일이에요.\n사이렌이 울리면 잠깐 멈추고 묵념해요."
  },
  {
    type: "ox",
    text: "현충일에는 집 밖에 태극기를 달아요.",
    illust: `<img src="https://upload.wikimedia.org/wikipedia/commons/0/09/Flag_of_South_Korea.svg" width="140" height="93" alt="대한민국 태극기" style="border:1px solid #D3D1C7; border-radius:4px;">`,
    illust_cap: "집에 태극기를 달아요",
    answer: "O",
    ok: "맞아요! 현충일에는 집 밖에 태극기를 달아\n감사한 마음을 표현해요.",
    no: "아쉬워요! 현충일에는 집 밖에 태극기를 달아요."
  },
  {
    type: "choice",
    text: "6·25 전쟁은 몇 년도에 시작됐나요?",
    illust: null,
    choices: ["1945년", "1950년", "1960년", "1919년"],
    answer: 1,
    ok: "정확해요! 6·25 전쟁은 1950년 6월 25일에\n시작됐어요.",
    no: "아쉬워요! 정답은 1950년이에요.\n1950년 6월 25일에 전쟁이 시작됐어요."
  },
  {
    type: "choice",
    text: "태극기를 들고 '대한 독립 만세!'를 외치며 독립운동을 이끈 분은 누구인가요?",
    illust: null,
    choices: ["이순신 장군", "세종대왕", "유관순 열사", "안중근 의사"],
    answer: 2,
    ok: "맞아요! 유관순 열사는 태극기를 들고\n독립운동을 이끈 용감한 분이에요.",
    no: "아쉬워요! 정답은 유관순 열사예요.\n태극기를 들고 만세를 외치며 독립운동을 이끌었어요."
  },
  {
    type: "choice",
    text: "우리나라가 일본으로부터 나라를 되찾은 날은 언제인가요?",
    illust: null,
    choices: ["3월 1일", "6월 6일", "7월 17일", "8월 15일"],
    answer: 3,
    ok: "완벽해요! 1945년 8월 15일, 드디어 나라를\n되찾았어요. 이 날을 광복절이라고 해요!",
    no: "아쉬워요! 정답은 8월 15일이에요.\n1945년 8월 15일에 광복을 맞이했어요."
  }
];

let cur = 0, score = 0, done = false;

function startQuiz() {
  cur = 0; score = 0; done = false;
  document.getElementById("quiz-section").style.display = "block";
  document.getElementById("result-card").style.display = "none";
  render();
}

function render() {
  done = false;
  const q = questions[cur];
  const total = questions.length;
  document.getElementById("prog").style.width = ((cur+1)/total*100)+"%";
  document.getElementById("prog-label").textContent = (cur+1)+" / "+total+" 문제";

  let h = `<span class="q-badge ${q.type==="ox"?"badge-ox":"badge-choice"}">${q.type==="ox"?"O / X 문제":"선택 문제"}</span>`;
  h += `<div class="q-text">${q.text}</div>`;
  if (q.illust) h += `<div class="q-illust">${q.illust}<div class="illust-cap">${q.illust_cap}</div></div>`;

  if (q.type==="ox") {
    h += `<div class="ox-row"><button class="ox-btn" id="bO" onclick="ansOX('O')">O</button><button class="ox-btn" id="bX" onclick="ansOX('X')">X</button></div>`;
  } else {
    h += `<div class="choice-list">`;
    q.choices.forEach((c,i) => {
      h += `<button class="choice-btn" id="b${i}" onclick="ansCh(${i})"><span class="num">${i+1}</span>${c}</button>`;
    });
    h += `</div>`;
  }
  h += `<div class="feedback" id="fb"></div>`;
  document.getElementById("q-card").innerHTML = h;

  const nb = document.getElementById("next-btn");
  nb.style.display = "none";
  nb.textContent = cur < questions.length-1 ? "다음 문제 →" : "결과 보기 →";
  nb.onclick = () => { cur++; cur < questions.length ? render() : showResult(); };
}

function showFB(correct) {
  const q = questions[cur];
  const fb = document.getElementById("fb");
  fb.className = "feedback "+(correct?"correct":"wrong");
  fb.textContent = (correct?"정답! ":"틀렸어요. ") + (correct?q.ok:q.no);
  fb.style.display = "block";
  document.getElementById("next-btn").style.display = "block";
}

function ansOX(v) {
  if (done) return; done = true;
  const q = questions[cur];
  const correct = v===q.answer;
  if (correct) score++;
  const bO = document.getElementById("bO");
  const bX = document.getElementById("bX");
  bO.className = "ox-btn " + (q.answer==="O" ? "correct" : (v==="O" ? "wrong" : ""));
  bX.className = "ox-btn " + (q.answer==="X" ? "correct" : (v==="X" ? "wrong" : ""));
  bO.disabled = bX.disabled = true;
  showFB(correct);
}

function ansCh(idx) {
  if (done) return; done = true;
  const q = questions[cur];
  const correct = idx===q.answer;
  if (correct) score++;
  q.choices.forEach((_,i) => {
    const b = document.getElementById("b"+i);
    b.className = "choice-btn " + (i===q.answer ? "correct" : (i===idx && !correct ? "wrong" : ""));
    b.disabled = true;
  });
  showFB(correct);
}

function showResult() {
  document.getElementById("quiz-section").style.display = "none";
  const rc = document.getElementById("result-card");
  rc.style.display = "block";
  document.getElementById("result-score").textContent = score+" / 5";
  let stars, msg;
  if      (score===5) { stars="★★★★★"; msg="완벽해요!\n역사 탐험가 인증!"; }
  else if (score>=4)  { stars="★★★★☆"; msg="정말 잘했어요!\n조금만 더 하면 완벽!"; }
  else if (score>=3)  { stars="★★★☆☆"; msg="잘했어요!\n책자를 다시 읽어 보면 더 잘할 수 있어요."; }
  else                { stars="★★☆☆☆"; msg="아쉬워요!\n책자를 다시 읽고 도전해 보세요."; }
  document.getElementById("result-stars").textContent = stars;
  document.getElementById("result-msg").textContent = msg;
}

startQuiz();
</script>
</body>
</html>
