<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Мессенджер</title>
  <script src="https://unpkg.com/mqtt/dist/mqtt.min.js"></script>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    :root {
      --bg: #f5f4f0; --surface: #ffffff; --surface2: #f0efe9;
      --border: rgba(0,0,0,0.1); --border2: rgba(0,0,0,0.18);
      --text: #1a1a18; --text2: #6b6b66; --text3: #9e9e97;
      --accent: #534AB7; --accent-dark: #3C3489;
      --green: #1D9E75; --red: #E24B4A;
      --radius: 12px; --radius-sm: 8px;
    }
    @media (prefers-color-scheme: dark) {
      :root {
        --bg: #1a1a18; --surface: #242422; --surface2: #2e2e2b;
        --border: rgba(255,255,255,0.1); --border2: rgba(255,255,255,0.18);
        --text: #f0efe9; --text2: #a0a09a; --text3: #6b6b66;
      }
    }
    html, body { height: 100%; background: var(--bg); font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif; color: var(--text); }
    body { display: flex; align-items: center; justify-content: center; padding: 16px; min-height: 100vh; }

    .app { width: 100%; max-width: 700px; height: calc(100vh - 32px); max-height: 720px; background: var(--surface); border: 0.5px solid var(--border); border-radius: var(--radius); overflow: hidden; display: flex; flex-direction: column; box-shadow: 0 4px 40px rgba(0,0,0,0.08); position: relative; }

    /* Header */
    .header { padding: 12px 18px; border-bottom: 0.5px solid var(--border); background: var(--surface2); display: flex; align-items: center; gap: 10px; flex-shrink: 0; }
    .logo { width: 32px; height: 32px; background: var(--accent); border-radius: 8px; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
    .logo svg { width: 18px; height: 18px; }
    .header-info { flex: 1; min-width: 0; }
    .header-title { font-size: 15px; font-weight: 600; color: var(--text); }
    .header-status { font-size: 12px; color: var(--text3); display: flex; align-items: center; gap: 5px; }
    .dot { width: 7px; height: 7px; border-radius: 50%; background: var(--text3); transition: background 0.3s; flex-shrink: 0; }
    .dot.on { background: var(--green); }
    .dot.err { background: var(--red); }
    .call-btn { background: var(--green); color: #fff; border: none; border-radius: 50%; width: 36px; height: 36px; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 18px; transition: background 0.15s, transform 0.1s; flex-shrink: 0; }
    .call-btn:hover { background: #17865f; transform: scale(1.05); }
    .call-btn:disabled { background: var(--surface2); color: var(--text3); cursor: not-allowed; transform: none; }
    .end-btn { background: var(--red); color: #fff; border: none; border-radius: 50%; width: 36px; height: 36px; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 18px; transition: background 0.15s; flex-shrink: 0; display: none; }
    .end-btn:hover { background: #c73b3a; }
    .mute-btn { background: var(--surface); border: 1px solid var(--border2); border-radius: 50%; width: 36px; height: 36px; display: flex; align-items: center; justify-content: center; cursor: pointer; font-size: 17px; transition: background 0.15s; flex-shrink: 0; display: none; }
    .mute-btn.muted { background: #FAECE7; border-color: var(--red); }

    /* Setup */
    .setup { padding: 10px 18px; border-bottom: 0.5px solid var(--border); background: var(--surface2); display: flex; gap: 8px; align-items: center; flex-shrink: 0; flex-wrap: wrap; }
    .setup label { font-size: 12px; color: var(--text2); white-space: nowrap; }
    .setup input { flex: 1; min-width: 80px; border: 0.5px solid var(--border2); border-radius: var(--radius-sm); padding: 6px 10px; font-size: 13px; color: var(--text); background: var(--surface); outline: none; transition: border-color 0.15s; }
    .setup input:focus { border-color: var(--accent); }
    .join-btn { background: var(--accent); color: #fff; border: none; border-radius: var(--radius-sm); padding: 6px 16px; font-size: 13px; font-weight: 500; cursor: pointer; white-space: nowrap; transition: background 0.15s; }
    .join-btn:hover { background: var(--accent-dark); }

    /* Room hint */
    .room-hint { padding: 5px 18px; font-size: 11px; color: var(--text3); background: var(--surface2); border-bottom: 0.5px solid var(--border); display: none; align-items: center; justify-content: center; gap: 6px; flex-shrink: 0; }
    .room-hint.visible { display: flex; }
    .copy-btn { background: none; border: none; color: var(--accent); font-size: 11px; cursor: pointer; text-decoration: underline; padding: 0; }

    /* Incoming call overlay */
    .call-overlay { position: absolute; top: 0; left: 0; right: 0; bottom: 0; background: rgba(0,0,0,0.6); backdrop-filter: blur(6px); display: none; align-items: center; justify-content: center; z-index: 100; }
    .call-overlay.visible { display: flex; }
    .call-card { background: var(--surface); border-radius: var(--radius); padding: 32px 40px; text-align: center; box-shadow: 0 8px 40px rgba(0,0,0,0.3); }
    .call-avatar { width: 70px; height: 70px; border-radius: 50%; background: var(--accent); display: flex; align-items: center; justify-content: center; font-size: 28px; color: #fff; margin: 0 auto 14px; animation: pulse 1.5s infinite; }
    @keyframes pulse { 0%,100%{box-shadow:0 0 0 0 rgba(83,74,183,0.4)} 50%{box-shadow:0 0 0 14px rgba(83,74,183,0)} }
    .call-name { font-size: 20px; font-weight: 600; color: var(--text); margin-bottom: 4px; }
    .call-label { font-size: 13px; color: var(--text3); margin-bottom: 28px; }
    .call-actions { display: flex; gap: 20px; justify-content: center; }
    .accept-btn { background: var(--green); color: #fff; border: none; border-radius: 50%; width: 58px; height: 58px; font-size: 26px; cursor: pointer; transition: background 0.15s, transform 0.1s; }
    .accept-btn:hover { background: #17865f; transform: scale(1.05); }
    .reject-btn { background: var(--red); color: #fff; border: none; border-radius: 50%; width: 58px; height: 58px; font-size: 26px; cursor: pointer; transition: background 0.15s, transform 0.1s; }
    .reject-btn:hover { background: #c73b3a; transform: scale(1.05); }

    /* Active call bar */
    .call-bar { background: linear-gradient(90deg, #1a6b4e, #175f44); color: #fff; padding: 8px 18px; display: none; align-items: center; gap: 10px; flex-shrink: 0; font-size: 13px; }
    .call-bar.visible { display: flex; }
    .call-timer { font-variant-numeric: tabular-nums; font-weight: 500; }
    .call-bar-spacer { flex: 1; }

    /* Visualizer */
    .audio-vis { display: flex; align-items: center; gap: 2px; height: 18px; }
    .audio-bar { width: 3px; border-radius: 2px; background: rgba(255,255,255,0.7); transition: height 0.1s; }

    /* Messages */
    .messages { flex: 1; overflow-y: auto; padding: 14px 18px; display: flex; flex-direction: column; gap: 10px; scroll-behavior: smooth; }
    .messages::-webkit-scrollbar { width: 4px; }
    .messages::-webkit-scrollbar-thumb { background: var(--border2); border-radius: 2px; }
    .sys-msg { text-align: center; font-size: 12px; color: var(--text3); padding: 2px 0; user-select: none; }
    .msg-group { display: flex; flex-direction: column; }
    .msg-group.me { align-items: flex-end; }
    .msg-group.them { align-items: flex-start; }
    .msg-name { font-size: 11px; color: var(--text2); margin-bottom: 3px; padding: 0 4px; }
    .bubble { max-width: 72%; padding: 9px 14px; border-radius: 16px; font-size: 14px; line-height: 1.55; word-break: break-word; }
    .bubble.me { background: var(--accent); color: #fff; border-bottom-right-radius: 4px; }
    .bubble.them { background: var(--surface2); color: var(--text); border-bottom-left-radius: 4px; border: 0.5px solid var(--border); }
    .msg-time { font-size: 11px; color: var(--text3); margin-top: 3px; padding: 0 4px; }

    /* Emoji + input */
    .emoji-bar { padding: 0 14px 6px; display: flex; gap: 4px; flex-shrink: 0; }
    .emoji-btn { background: none; border: none; font-size: 20px; cursor: pointer; border-radius: 6px; padding: 2px 4px; transition: background 0.1s; }
    .emoji-btn:hover { background: var(--surface2); }
    .input-area { padding: 10px 14px; border-top: 0.5px solid var(--border); background: var(--surface); display: flex; gap: 8px; align-items: flex-end; flex-shrink: 0; }
    .msg-input { flex: 1; border: 0.5px solid var(--border2); border-radius: 20px; padding: 9px 16px; font-size: 14px; color: var(--text); background: var(--surface2); outline: none; resize: none; min-height: 38px; max-height: 120px; font-family: inherit; line-height: 1.4; transition: border-color 0.15s; }
    .msg-input:focus { border-color: var(--accent); }
    .msg-input:disabled { opacity: 0.5; cursor: not-allowed; }
    .send-btn { width: 38px; height: 38px; border-radius: 50%; background: var(--accent); border: none; cursor: pointer; display: flex; align-items: center; justify-content: center; flex-shrink: 0; transition: background 0.15s, transform 0.1s; }
    .send-btn:hover { background: var(--accent-dark); }
    .send-btn:active { transform: scale(0.95); }
    .send-btn:disabled { background: var(--surface2); cursor: not-allowed; }
    .send-btn svg { width: 16px; height: 16px; fill: #fff; }
    .send-btn:disabled svg { fill: var(--text3); }

    @media (max-width: 500px) {
      body { padding: 0; }
      .app { max-height: 100vh; height: 100vh; border-radius: 0; border: none; }
    }
  </style>
</head>
<body>
<div class="app">

  <!-- Incoming call overlay -->
  <div class="call-overlay" id="callOverlay">
    <div class="call-card">
      <div class="call-avatar" id="callerAvatar">📞</div>
      <div class="call-name" id="callerName">Входящий звонок</div>
      <div class="call-label">Голосовой вызов</div>
      <div class="call-actions">
        <button class="accept-btn" onclick="acceptCall()" title="Принять">📞</button>
        <button class="reject-btn" onclick="rejectCall()" title="Отклонить">📵</button>
      </div>
    </div>
  </div>

  <!-- Header -->
  <div class="header">
    <div class="logo">
      <svg viewBox="0 0 24 24" fill="none">
        <path d="M21 15a2 2 0 0 1-2 2H7l-4 4V5a2 2 0 0 1 2-2h14a2 2 0 0 1 2 2z" stroke="#fff" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
      </svg>
    </div>
    <div class="header-info">
      <div class="header-title" id="headerTitle">Мессенджер</div>
      <div class="header-status">
        <div class="dot" id="dot"></div>
        <span id="statusText">Введите имя и ID комнаты</span>
      </div>
    </div>
    <button class="mute-btn" id="muteBtn" onclick="toggleMute()" title="Микрофон">🎙️</button>
    <button class="end-btn" id="endBtn" onclick="endCall()" title="Завершить звонок">📵</button>
    <button class="call-btn" id="callBtn" onclick="startCall()" disabled title="Голосовой звонок">📞</button>
  </div>

  <!-- Active call bar -->
  <div class="call-bar" id="callBar">
    <span>🟢 Звонок активен</span>
    <div class="audio-vis" id="audioVis">
      <div class="audio-bar" style="height:6px"></div>
      <div class="audio-bar" style="height:10px"></div>
      <div class="audio-bar" style="height:14px"></div>
      <div class="audio-bar" style="height:10px"></div>
      <div class="audio-bar" style="height:6px"></div>
    </div>
    <span class="call-bar-spacer"></span>
    <span class="call-timer" id="callTimer">0:00</span>
  </div>

  <!-- Setup -->
  <div class="setup">
    <label>Имя:</label>
    <input id="nameInput" placeholder="Псевдоним" maxlength="20" style="max-width:150px;" />
    <label>Комната:</label>
    <input id="roomInput" placeholder="ID комнаты" maxlength="40" />
    <button class="join-btn" id="joinBtn" onclick="joinRoom()">Войти</button>
  </div>

  <div class="room-hint" id="roomHint">
    Комната: <strong id="hintRoom"></strong> —
    <button class="copy-btn" onclick="copyRoom()">скопировать ID</button>
    и отправить собеседнику
  </div>

  <!-- Messages -->
  <div class="messages" id="messages">
    <div class="sys-msg">👋 Введите имя и ID комнаты выше, чтобы начать</div>
    <div class="sys-msg">Оба собеседника вводят одинаковый ID комнаты</div>
    <div class="sys-msg">📞 Кнопка звонка появится после подключения</div>
  </div>

  <!-- Emoji -->
  <div class="emoji-bar">
    <button class="emoji-btn" onclick="insertEmoji('😊')">😊</button>
    <button class="emoji-btn" onclick="insertEmoji('👍')">👍</button>
    <button class="emoji-btn" onclick="insertEmoji('❤️')">❤️</button>
    <button class="emoji-btn" onclick="insertEmoji('😂')">😂</button>
    <button class="emoji-btn" onclick="insertEmoji('🔥')">🔥</button>
    <button class="emoji-btn" onclick="insertEmoji('👋')">👋</button>
    <button class="emoji-btn" onclick="insertEmoji('🎉')">🎉</button>
    <button class="emoji-btn" onclick="insertEmoji('😢')">😢</button>
  </div>

  <!-- Input -->
  <div class="input-area">
    <textarea class="msg-input" id="msgInput" placeholder="Напишите сообщение... (Enter — отправить)" rows="1" disabled></textarea>
    <button class="send-btn" id="sendBtn" disabled onclick="sendMsg()">
      <svg viewBox="0 0 24 24"><path d="M22 2L11 13M22 2L15 22L11 13M22 2L2 9L11 13"/></svg>
    </button>
  </div>
</div>

<audio id="remoteAudio" autoplay playsinline></audio>

<script>
// ─── State ─────────────────────────────────────────────────────────────
let mqttClient = null, currentRoom = null;
let myName = 'Аноним', myId = Math.random().toString(36).slice(2, 10);

// WebRTC
let pc = null, localStream = null;
let isCalling = false, inCall = false;
let callTimerInterval = null, callSeconds = 0;
let pendingOffer = null, callerInfo = null;
let audioContext = null, analyser = null, visInterval = null;
let isMuted = false;

// ICE servers (STUN) — публичные серверы
const ICE_SERVERS = {
  iceServers: [
    { urls: 'stun:stun.l.google.com:19302' },
    { urls: 'stun:stun1.l.google.com:19302' },
    { urls: 'stun:stun.cloudflare.com:3478' },
  ]
};

// ─── Init ───────────────────────────────────────────────────────────────
const adj = ['Весёлый','Быстрый','Умный','Яркий','Добрый','Храбрый','Мудрый'];
const nou = ['Кот','Волк','Орёл','Лис','Медведь','Тигр','Сова'];
document.getElementById('nameInput').value = adj[Math.floor(Math.random()*adj.length)] + nou[Math.floor(Math.random()*nou.length)];
document.getElementById('roomInput').value = Math.random().toString(36).slice(2, 8);

function ts() {
  const d = new Date();
  return d.getHours().toString().padStart(2,'0') + ':' + d.getMinutes().toString().padStart(2,'0');
}

function addSys(text) {
  const el = document.getElementById('messages');
  const d = document.createElement('div');
  d.className = 'sys-msg'; d.textContent = text;
  el.appendChild(d); el.scrollTop = el.scrollHeight;
}

function addMsg(name, text, isMe) {
  const el = document.getElementById('messages');
  const group = document.createElement('div');
  group.className = 'msg-group ' + (isMe ? 'me' : 'them');
  if (!isMe) {
    const n = document.createElement('div'); n.className = 'msg-name'; n.textContent = name;
    group.appendChild(n);
  }
  const b = document.createElement('div');
  b.className = 'bubble ' + (isMe ? 'me' : 'them'); b.textContent = text;
  group.appendChild(b);
  const t = document.createElement('div'); t.className = 'msg-time'; t.textContent = ts();
  group.appendChild(t);
  el.appendChild(group); el.scrollTop = el.scrollHeight;
}

function setStatus(state, text) {
  document.getElementById('dot').className = 'dot' + (state === 'on' ? ' on' : state === 'err' ? ' err' : '');
  document.getElementById('statusText').textContent = text;
}

// ─── MQTT ────────────────────────────────────────────────────────────────
function publish(subtopic, data) {
  if (!mqttClient || !currentRoom) return;
  mqttClient.publish(currentRoom + '/' + subtopic, JSON.stringify(data), { qos: 1 });
}

function joinRoom() {
  const rawRoom = document.getElementById('roomInput').value.trim().replace(/[^a-zA-Z0-9\-_а-яёА-ЯЁ]/gi, '');
  const name = document.getElementById('nameInput').value.trim() || 'Аноним';
  if (!rawRoom) { alert('Введите ID комнаты!'); return; }
  myName = name;
  currentRoom = 'claudemsg_v2/' + rawRoom;
  document.getElementById('headerTitle').textContent = 'Комната: ' + rawRoom;
  document.getElementById('hintRoom').textContent = rawRoom;
  document.getElementById('roomHint').classList.add('visible');
  setStatus('', 'Подключение...');
  if (mqttClient) { try { mqttClient.end(true); } catch(e){} mqttClient = null; }

  const brokers = ['wss://broker.hivemq.com:8884/mqtt', 'wss://test.mosquitto.org:8081/mqtt'];
  function tryBroker(idx) {
    if (idx >= brokers.length) { setStatus('err', 'Ошибка подключения'); addSys('❌ Нет соединения.'); return; }
    setStatus('', 'Подключение ' + (idx+1) + '/' + brokers.length + '...');
    const c = mqtt.connect(brokers[idx], { clientId: 'cm_' + myId + '_' + Date.now(), reconnectPeriod: 0, connectTimeout: 8000, keepalive: 30, clean: true });
    const timer = setTimeout(() => { c.end(true); tryBroker(idx+1); }, 9000);
    c.on('connect', () => {
      clearTimeout(timer); mqttClient = c;
      setStatus('on', 'Подключено • ' + myName);
      ['msg','sys','signal'].forEach(t => c.subscribe(currentRoom+'/'+t, { qos: 1 }));
      document.getElementById('msgInput').disabled = false;
      document.getElementById('sendBtn').disabled = false;
      document.getElementById('callBtn').disabled = false;
      document.getElementById('joinBtn').textContent = 'Сменить';
      document.getElementById('msgInput').focus();
      publish('sys', { id: myId, name: myName, action: 'join' });
      addSys('✅ Вы в комнате как «' + myName + '». 📞 Кнопка звонка активна!');
    });
    c.on('message', (topic, payload) => {
      try {
        const data = JSON.parse(payload.toString());
        if (topic.endsWith('/msg')) { if (data.id !== myId) addMsg(data.name, data.text, false); }
        else if (topic.endsWith('/sys')) {
          if (data.id === myId) return;
          if (data.action === 'join') addSys('👤 ' + data.name + ' вошёл(а) в комнату');
          if (data.action === 'leave') addSys('👤 ' + data.name + ' покинул(а) комнату');
        }
        else if (topic.endsWith('/signal')) { handleSignal(data); }
      } catch(e) {}
    });
    c.on('error', () => { clearTimeout(timer); c.end(true); setTimeout(() => tryBroker(idx+1), 300); });
    c.on('close', () => {
      if (mqttClient === c) {
        setStatus('err', 'Соединение разорвано');
        document.getElementById('msgInput').disabled = true;
        document.getElementById('sendBtn').disabled = true;
        document.getElementById('callBtn').disabled = true;
      }
    });
  }
  tryBroker(0);
}

// ─── Messaging ────────────────────────────────────────────────────────────
function sendMsg() {
  const input = document.getElementById('msgInput');
  const text = input.value.trim();
  if (!text || !mqttClient) return;
  publish('msg', { id: myId, name: myName, text });
  addMsg(myName, text, true);
  input.value = ''; input.style.height = 'auto';
}

// ─── WebRTC Signaling ─────────────────────────────────────────────────────
async function handleSignal(data) {
  if (data.to && data.to !== myId) return; // not for us

  if (data.type === 'offer') {
    if (inCall) { publish('signal', { type: 'busy', to: data.from, from: myId }); return; }
    pendingOffer = data;
    callerInfo = { name: data.name, id: data.from };
    document.getElementById('callerName').textContent = data.name;
    document.getElementById('callerAvatar').textContent = '📞';
    document.getElementById('callOverlay').classList.add('visible');
    addSys('📞 Входящий звонок от ' + data.name + '...');
  }
  else if (data.type === 'answer' && pc) {
    await pc.setRemoteDescription(new RTCSessionDescription({ type: 'answer', sdp: data.sdp }));
    addSys('✅ Звонок принят — соединение установлено');
  }
  else if (data.type === 'ice' && pc) {
    try { await pc.addIceCandidate(new RTCIceCandidate(data.candidate)); } catch(e) {}
  }
  else if (data.type === 'hangup') {
    addSys('📵 Собеседник завершил звонок');
    cleanupCall();
  }
  else if (data.type === 'reject') {
    addSys('❌ Звонок отклонён');
    cleanupCall();
  }
  else if (data.type === 'busy') {
    addSys('⚠️ Собеседник занят');
    cleanupCall();
  }
}

async function createPC(isInitiator) {
  pc = new RTCPeerConnection(ICE_SERVERS);

  pc.onicecandidate = e => {
    if (e.candidate) {
      publish('signal', { type: 'ice', candidate: e.candidate, from: myId, name: myName });
    }
  };

  pc.ontrack = e => {
    document.getElementById('remoteAudio').srcObject = e.streams[0];
    startCallUI();
    startVisualizer(e.streams[0]);
  };

  pc.onconnectionstatechange = () => {
    if (pc && (pc.connectionState === 'failed' || pc.connectionState === 'disconnected')) {
      addSys('⚠️ Соединение прервано');
      cleanupCall();
    }
  };

  try {
    localStream = await navigator.mediaDevices.getUserMedia({ audio: true, video: false });
    localStream.getTracks().forEach(t => pc.addTrack(t, localStream));
  } catch(e) {
    addSys('❌ Нет доступа к микрофону: ' + e.message);
    cleanupCall();
    throw e;
  }
  return pc;
}

async function startCall() {
  if (inCall || isCalling) return;
  isCalling = true;
  addSys('📞 Вызов... (ожидание собеседника)');
  document.getElementById('callBtn').disabled = true;

  try {
    await createPC(true);
    const offer = await pc.createOffer({ offerToReceiveAudio: true });
    await pc.setLocalDescription(offer);
    publish('signal', { type: 'offer', sdp: offer.sdp, from: myId, name: myName });
  } catch(e) {
    addSys('❌ Ошибка при звонке: ' + e.message);
    cleanupCall();
  }
}

async function acceptCall() {
  document.getElementById('callOverlay').classList.remove('visible');
  if (!pendingOffer) return;

  try {
    await createPC(false);
    await pc.setRemoteDescription(new RTCSessionDescription({ type: 'offer', sdp: pendingOffer.sdp }));
    const answer = await pc.createAnswer();
    await pc.setLocalDescription(answer);
    publish('signal', { type: 'answer', sdp: answer.sdp, to: pendingOffer.from, from: myId, name: myName });
    inCall = true; isCalling = false;
    startCallUI();
    addSys('📞 Звонок принят');
  } catch(e) {
    addSys('❌ Ошибка принятия звонка: ' + e.message);
    cleanupCall();
  }
  pendingOffer = null;
}

function rejectCall() {
  document.getElementById('callOverlay').classList.remove('visible');
  if (callerInfo) {
    publish('signal', { type: 'reject', to: callerInfo.id, from: myId, name: myName });
    addSys('📵 Звонок отклонён');
  }
  pendingOffer = null; callerInfo = null;
}

function endCall() {
  publish('signal', { type: 'hangup', from: myId, name: myName });
  addSys('📵 Вы завершили звонок');
  cleanupCall();
}

function cleanupCall() {
  isCalling = false; inCall = false;
  if (localStream) { localStream.getTracks().forEach(t => t.stop()); localStream = null; }
  if (pc) { pc.close(); pc = null; }
  document.getElementById('remoteAudio').srcObject = null;
  document.getElementById('callOverlay').classList.remove('visible');
  stopCallUI();
  stopVisualizer();
  pendingOffer = null; callerInfo = null; isMuted = false;
}

function startCallUI() {
  inCall = true; isCalling = false;
  document.getElementById('callBar').classList.add('visible');
  document.getElementById('callBtn').style.display = 'none';
  document.getElementById('endBtn').style.display = 'flex';
  document.getElementById('muteBtn').style.display = 'flex';
  callSeconds = 0;
  clearInterval(callTimerInterval);
  callTimerInterval = setInterval(() => {
    callSeconds++;
    const m = Math.floor(callSeconds/60), s = callSeconds%60;
    document.getElementById('callTimer').textContent = m + ':' + s.toString().padStart(2,'0');
  }, 1000);
}

function stopCallUI() {
  document.getElementById('callBar').classList.remove('visible');
  document.getElementById('callBtn').style.display = '';
  document.getElementById('callBtn').disabled = false;
  document.getElementById('endBtn').style.display = 'none';
  document.getElementById('muteBtn').style.display = 'none';
  clearInterval(callTimerInterval);
}

function toggleMute() {
  if (!localStream) return;
  isMuted = !isMuted;
  localStream.getAudioTracks().forEach(t => t.enabled = !isMuted);
  const btn = document.getElementById('muteBtn');
  btn.textContent = isMuted ? '🔇' : '🎙️';
  btn.classList.toggle('muted', isMuted);
  addSys(isMuted ? '🔇 Микрофон выключен' : '🎙️ Микрофон включён');
}

// ─── Audio Visualizer ─────────────────────────────────────────────────────
function startVisualizer(stream) {
  try {
    audioContext = new (window.AudioContext || window.webkitAudioContext)();
    analyser = audioContext.createAnalyser();
    analyser.fftSize = 64;
    const src = audioContext.createMediaStreamSource(stream);
    src.connect(analyser);
    const bars = document.querySelectorAll('.audio-bar');
    const data = new Uint8Array(analyser.frequencyBinCount);
    visInterval = setInterval(() => {
      analyser.getByteFrequencyData(data);
      bars.forEach((b, i) => {
        const v = data[i*2] || 0;
        b.style.height = Math.max(4, (v / 255) * 18) + 'px';
      });
    }, 80);
  } catch(e) {}
}

function stopVisualizer() {
  clearInterval(visInterval);
  if (audioContext) { audioContext.close().catch(()=>{}); audioContext = null; }
  document.querySelectorAll('.audio-bar').forEach((b,i) => {
    b.style.height = [6,10,14,10,6][i] + 'px';
  });
}

// ─── Utils ────────────────────────────────────────────────────────────────
function copyRoom() {
  const id = document.getElementById('roomInput').value.trim().replace(/[^a-zA-Z0-9\-_а-яёА-ЯЁ]/gi,'');
  navigator.clipboard.writeText(id).then(() => {
    const btn = document.querySelector('.copy-btn');
    const orig = btn.textContent; btn.textContent = '✓ скопировано!';
    setTimeout(() => btn.textContent = orig, 2000);
  });
}

function insertEmoji(e) {
  const input = document.getElementById('msgInput');
  if (input.disabled) return;
  const s = input.selectionStart, end = input.selectionEnd;
  input.value = input.value.slice(0,s) + e + input.value.slice(end);
  input.selectionStart = input.selectionEnd = s + e.length;
  input.focus();
}

document.getElementById('msgInput').addEventListener('keydown', e => {
  if (e.key === 'Enter' && !e.shiftKey) { e.preventDefault(); sendMsg(); }
});
document.getElementById('msgInput').addEventListener('input', function() {
  this.style.height = 'auto';
  this.style.height = Math.min(this.scrollHeight, 120) + 'px';
});
document.getElementById('roomInput').addEventListener('keydown', e => {
  if (e.key === 'Enter') joinRoom();
});
window.addEventListener('beforeunload', () => {
  if (inCall) endCall();
  if (mqttClient && currentRoom) {
    try { publish('sys', { id: myId, name: myName, action: 'leave' }); } catch(e) {}
  }
});
</script>
</body>
</html>
