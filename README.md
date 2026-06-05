<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Nexus — Réseau Social</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Clash+Display:wght@400;500;600;700&family=Syne:wght@400;500;600;700;800&family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;1,9..40,300&display=swap" rel="stylesheet">
<style>
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

:root {
  --bg: #080810;
  --bg2: #0f0f1a;
  --bg3: #161625;
  --bg4: #1e1e30;
  --bg5: #252538;
  --border: rgba(255,255,255,0.06);
  --border2: rgba(255,255,255,0.12);
  --border3: rgba(255,255,255,0.2);
  --text: #eeeef8;
  --text2: rgba(238,238,248,0.75);
  --muted: #6b6b8a;
  --muted2: #3d3d5a;
  --accent: #6c4ef2;
  --accent2: #8b6fff;
  --accent3: #b8a3ff;
  --glow: rgba(108,78,242,0.25);
  --pink: #e8629a;
  --pink2: rgba(232,98,154,0.15);
  --teal: #22d3a0;
  --amber: #f5a623;
  --red: #ef4444;
  --green: #22c55e;
  --font-head: 'Syne', sans-serif;
  --font-body: 'DM Sans', sans-serif;
  --r: 12px;
  --r2: 18px;
  --r3: 24px;
  --sidebar-w: 260px;
  --aside-w: 310px;
  --transition: 0.18s ease;
}

html, body { height: 100%; background: var(--bg); color: var(--text); font-family: var(--font-body); font-size: 15px; line-height: 1.6; overflow-x: hidden; }

::-webkit-scrollbar { width: 3px; }
::-webkit-scrollbar-track { background: transparent; }
::-webkit-scrollbar-thumb { background: var(--bg5); border-radius: 2px; }

/* ── NOISE TEXTURE ── */
body::before {
  content: ''; position: fixed; inset: 0; pointer-events: none; z-index: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
  opacity: 0.4;
}

/* ── AUTH ── */
#auth-screen {
  min-height: 100vh; display: flex; align-items: center; justify-content: center; position: relative; z-index: 1;
  background:
    radial-gradient(ellipse 70% 60% at 20% 30%, rgba(108,78,242,0.18) 0%, transparent 60%),
    radial-gradient(ellipse 50% 50% at 80% 70%, rgba(232,98,154,0.12) 0%, transparent 60%),
    radial-gradient(ellipse 40% 40% at 50% 10%, rgba(34,211,160,0.08) 0%, transparent 60%);
}

.auth-orbs {
  position: absolute; inset: 0; pointer-events: none; overflow: hidden;
}
.auth-orb {
  position: absolute; border-radius: 50%; filter: blur(80px); animation: orbFloat 8s ease-in-out infinite;
}
.auth-orb:nth-child(1) { width: 400px; height: 400px; background: rgba(108,78,242,0.12); top: -100px; left: -100px; animation-delay: 0s; }
.auth-orb:nth-child(2) { width: 300px; height: 300px; background: rgba(232,98,154,0.1); bottom: -50px; right: -50px; animation-delay: -3s; }
.auth-orb:nth-child(3) { width: 200px; height: 200px; background: rgba(34,211,160,0.08); top: 50%; left: 60%; animation-delay: -5s; }
@keyframes orbFloat { 0%,100% { transform: translateY(0) scale(1); } 50% { transform: translateY(-30px) scale(1.05); } }

.auth-box {
  width: 440px; background: rgba(15,15,26,0.9); border: 1px solid var(--border2); border-radius: var(--r3);
  padding: 2.75rem; position: relative; overflow: hidden; backdrop-filter: blur(20px);
  box-shadow: 0 32px 80px rgba(0,0,0,0.5), 0 0 0 1px rgba(255,255,255,0.04) inset;
  animation: authIn 0.5s cubic-bezier(0.16,1,0.3,1);
}
@keyframes authIn { from { opacity:0; transform: translateY(20px) scale(0.97); } to { opacity:1; transform:none; } }
.auth-box::before {
  content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, transparent, var(--accent), var(--pink), var(--teal), transparent);
}

.auth-logo { font-family: var(--font-head); font-size: 2.2rem; font-weight: 800; letter-spacing: -0.03em; margin-bottom: 0.2rem; }
.auth-logo .logo-dot { background: linear-gradient(135deg, var(--accent2), var(--pink)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }
.auth-sub { color: var(--muted); font-size: 0.9rem; margin-bottom: 2rem; font-weight: 300; }

.auth-tabs { display: flex; background: var(--bg3); border-radius: var(--r); padding: 4px; margin-bottom: 1.75rem; gap: 4px; }
.auth-tab { flex: 1; padding: 0.55rem; text-align: center; font-size: 0.875rem; font-weight: 500; cursor: pointer; color: var(--muted); transition: all var(--transition); background: transparent; border: none; font-family: var(--font-body); border-radius: 9px; }
.auth-tab.active { background: var(--accent); color: white; box-shadow: 0 2px 12px var(--glow); }

label { display: block; font-size: 0.78rem; font-weight: 600; color: var(--muted); margin-bottom: 0.4rem; text-transform: uppercase; letter-spacing: 0.07em; }

input[type=text], input[type=email], input[type=password], textarea, select {
  width: 100%; background: var(--bg3); border: 1px solid var(--border); border-radius: var(--r); padding: 0.75rem 1rem;
  color: var(--text); font-family: var(--font-body); font-size: 0.925rem; outline: none;
  transition: border-color var(--transition), box-shadow var(--transition), background var(--transition); margin-bottom: 1rem;
}
input:focus, textarea:focus, select:focus {
  border-color: var(--accent); box-shadow: 0 0 0 3px rgba(108,78,242,0.15);
  background: var(--bg4);
}
input::placeholder, textarea::placeholder { color: var(--muted2); }

.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: 0.5rem;
  padding: 0.75rem 1.25rem; border-radius: var(--r); font-family: var(--font-body); font-size: 0.9rem;
  font-weight: 600; cursor: pointer; border: none; transition: all var(--transition); text-decoration: none; white-space: nowrap;
}
.btn-primary { background: var(--accent); color: white; width: 100%; box-shadow: 0 4px 20px var(--glow); }
.btn-primary:hover { background: #7c5ef8; transform: translateY(-1px); box-shadow: 0 8px 28px rgba(108,78,242,0.4); }
.btn-primary:active { transform: translateY(0); }
.btn-ghost { background: transparent; color: var(--muted); border: 1px solid var(--border); }
.btn-ghost:hover { border-color: var(--border2); color: var(--text); background: var(--bg3); }
.btn-sm { padding: 0.4rem 0.875rem; font-size: 0.82rem; }
.btn-danger { background: rgba(239,68,68,0.12); color: var(--red); border: 1px solid rgba(239,68,68,0.2); }
.btn-danger:hover { background: rgba(239,68,68,0.22); }
.btn-teal { background: rgba(34,211,160,0.12); color: var(--teal); border: 1px solid rgba(34,211,160,0.2); }
.btn-teal:hover { background: rgba(34,211,160,0.22); }

.auth-err { color: var(--red); font-size: 0.85rem; margin-bottom: 0.75rem; display: none; background: rgba(239,68,68,0.08); border: 1px solid rgba(239,68,68,0.2); padding: 0.6rem 0.875rem; border-radius: 8px; }
.auth-err.show { display: block; }

.av-pick { display: flex; gap: 0.6rem; flex-wrap: wrap; margin-bottom: 1rem; }
.av-opt { width: 44px; height: 44px; border-radius: 50%; cursor: pointer; border: 2px solid transparent; transition: all var(--transition); font-size: 1.35rem; display: flex; align-items: center; justify-content: center; }
.av-opt:hover { transform: scale(1.1); }
.av-opt.selected { border-color: var(--accent); transform: scale(1.15); box-shadow: 0 0 0 3px var(--glow); }

/* ── APP ── */
#app { display: none; min-height: 100vh; position: relative; z-index: 1; }
.layout { display: grid; grid-template-columns: var(--sidebar-w) 1fr var(--aside-w); min-height: 100vh; max-width: 1320px; margin: 0 auto; }

/* ── SIDEBAR ── */
.sidebar {
  position: sticky; top: 0; height: 100vh; padding: 1.5rem 1rem; display: flex; flex-direction: column; gap: 0.2rem;
  border-right: 1px solid var(--border); overflow-y: auto;
}
.logo { font-family: var(--font-head); font-size: 1.65rem; font-weight: 800; letter-spacing: -0.03em; padding: 0.5rem 0.75rem; margin-bottom: 1.25rem; cursor: pointer; }
.logo .logo-dot { background: linear-gradient(135deg, var(--accent2), var(--pink)); -webkit-background-clip: text; -webkit-text-fill-color: transparent; background-clip: text; }

.nav-item {
  display: flex; align-items: center; gap: 0.875rem; padding: 0.75rem 0.875rem; border-radius: var(--r); cursor: pointer;
  color: var(--muted); font-weight: 500; font-size: 0.925rem; transition: all var(--transition); border: none; background: none; width: 100%; text-align: left; position: relative;
}
.nav-item:hover { color: var(--text); background: var(--bg3); }
.nav-item.active { color: var(--text); background: var(--bg3); }
.nav-item.active::before { content:''; position:absolute; left:0; top:20%; bottom:20%; width:3px; border-radius:0 2px 2px 0; background: var(--accent); }
.nav-icon { font-size: 1.2rem; flex-shrink: 0; width: 24px; text-align: center; }
.nav-badge { margin-left: auto; background: var(--accent); color: white; font-size: 0.68rem; font-weight: 700; padding: 2px 6px; border-radius: 99px; min-width: 20px; text-align: center; }
.nav-label { flex: 1; }

.sidebar-divider { height: 1px; background: var(--border); margin: 0.5rem 0.875rem; }

.sidebar-user {
  margin-top: auto; display: flex; align-items: center; gap: 0.75rem; padding: 0.875rem; border-radius: var(--r);
  background: var(--bg3); border: 1px solid var(--border); cursor: pointer; transition: all var(--transition);
}
.sidebar-user:hover { border-color: var(--border2); background: var(--bg4); }

/* ── AVATAR ── */
.avatar { border-radius: 50%; display: flex; align-items: center; justify-content: center; flex-shrink: 0; border: 2px solid var(--border2); transition: transform var(--transition); cursor: pointer; }
.avatar:hover { transform: scale(1.05); }
.avatar.sz-sm { width: 32px; height: 32px; font-size: 1rem; }
.avatar.sz-md { width: 40px; height: 40px; font-size: 1.25rem; }
.avatar.sz-lg { width: 52px; height: 52px; font-size: 1.5rem; }
.avatar.sz-xl { width: 80px; height: 80px; font-size: 2.2rem; border-width: 3px; }
.avatar.sz-xxl { width: 104px; height: 104px; font-size: 2.75rem; border-width: 4px; border-color: var(--bg); box-shadow: 0 0 0 3px var(--accent); }

/* ── FEED ── */
.feed { border-right: 1px solid var(--border); min-height: 100vh; }
.feed-header {
  position: sticky; top: 0; background: rgba(8,8,16,0.85); backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border); padding: 1rem 1.5rem; z-index: 10;
  display: flex; align-items: center; justify-content: space-between;
}
.feed-title { font-family: var(--font-head); font-size: 1.15rem; font-weight: 700; }
.feed-tabs { display: flex; border-bottom: 1px solid var(--border); }
.feed-tab { flex: 1; padding: 0.875rem; text-align: center; font-size: 0.875rem; font-weight: 500; cursor: pointer; color: var(--muted); border: none; background: none; border-bottom: 2px solid transparent; margin-bottom: -1px; transition: all var(--transition); font-family: var(--font-body); }
.feed-tab.active { color: var(--accent2); border-bottom-color: var(--accent); }
.feed-tab:hover:not(.active) { color: var(--text2); }

/* ── COMPOSE ── */
.compose { padding: 1.25rem 1.5rem; border-bottom: 1px solid var(--border); display: flex; gap: 0.875rem; align-items: flex-start; }
.compose-area { flex: 1; }
.compose-area textarea { margin-bottom: 0.75rem; resize: none; min-height: 88px; font-size: 1rem; line-height: 1.6; }
.compose-footer { display: flex; justify-content: space-between; align-items: center; }
.compose-tools { display: flex; gap: 0.25rem; }
.compose-tool { background: none; border: none; color: var(--muted); cursor: pointer; padding: 0.4rem; border-radius: 8px; font-size: 1.05rem; transition: all var(--transition); }
.compose-tool:hover { color: var(--accent2); background: rgba(108,78,242,0.1); }
.char-count { font-size: 0.8rem; color: var(--muted); font-variant-numeric: tabular-nums; }
.char-count.warn { color: var(--amber); }
.char-count.over { color: var(--red); }

/* mood selector */
.mood-bar { display: flex; gap: 0.5rem; margin-bottom: 0.75rem; flex-wrap: wrap; }
.mood-chip { padding: 0.3rem 0.7rem; border-radius: 99px; font-size: 0.78rem; cursor: pointer; border: 1px solid var(--border); background: transparent; color: var(--muted); transition: all var(--transition); font-family: var(--font-body); }
.mood-chip:hover { border-color: var(--border2); color: var(--text); }
.mood-chip.selected { border-color: var(--accent); background: rgba(108,78,242,0.15); color: var(--accent3); }

/* ── POST ── */
.post { padding: 1.25rem 1.5rem; border-bottom: 1px solid var(--border); transition: background var(--transition); animation: postIn 0.3s ease; }
@keyframes postIn { from { opacity:0; transform: translateY(-6px); } to { opacity:1; transform:none; } }
.post:hover { background: rgba(255,255,255,0.012); }
.post-wrap { position: relative; }

.post-header { display: flex; align-items: flex-start; gap: 0.875rem; margin-bottom: 0.875rem; }
.post-meta { flex: 1; min-width: 0; }
.post-name { font-weight: 600; font-size: 0.95rem; cursor: pointer; }
.post-name:hover { color: var(--accent2); text-decoration: underline; }
.post-handle { color: var(--muted); font-size: 0.82rem; }
.post-time { color: var(--muted2); font-size: 0.78rem; }
.post-mood { font-size: 0.75rem; color: var(--muted); margin-top: 0.1rem; }
.post-body { font-size: 0.95rem; line-height: 1.7; margin-bottom: 0.875rem; word-break: break-word; white-space: pre-wrap; color: var(--text2); }
.post-body .mention { color: var(--accent2); cursor: pointer; font-weight: 500; }
.post-body .mention:hover { text-decoration: underline; }
.post-image { width: 100%; max-height: 340px; object-fit: cover; border-radius: var(--r); margin-bottom: 0.875rem; border: 1px solid var(--border); }
.post-tag { display: inline-block; background: rgba(108,78,242,0.1); color: var(--accent3); padding: 2px 10px; border-radius: 99px; font-size: 0.78rem; margin-right: 0.3rem; margin-bottom: 0.4rem; cursor: pointer; transition: background var(--transition); font-weight: 500; }
.post-tag:hover { background: rgba(108,78,242,0.22); }

/* Poll */
.poll { background: var(--bg3); border-radius: var(--r); padding: 1rem; margin-bottom: 0.875rem; border: 1px solid var(--border); }
.poll-option { display: flex; align-items: center; gap: 0.75rem; margin-bottom: 0.5rem; cursor: pointer; padding: 0.5rem 0.75rem; border-radius: 8px; border: 1px solid var(--border2); transition: all var(--transition); position: relative; overflow: hidden; }
.poll-option:last-child { margin-bottom: 0; }
.poll-option:hover:not(.voted) { border-color: var(--accent); background: rgba(108,78,242,0.05); }
.poll-option.voted { cursor: default; }
.poll-option.winner { border-color: var(--accent); }
.poll-bar { position: absolute; left: 0; top: 0; bottom: 0; background: rgba(108,78,242,0.12); transition: width 0.5s ease; border-radius: 8px; }
.poll-label { position: relative; flex: 1; font-size: 0.875rem; }
.poll-pct { position: relative; font-size: 0.8rem; color: var(--muted); font-variant-numeric: tabular-nums; }
.poll-info { font-size: 0.78rem; color: var(--muted2); margin-top: 0.5rem; }

.post-actions { display: flex; gap: 0.5rem; flex-wrap: wrap; }
.post-action {
  display: flex; align-items: center; gap: 0.35rem; color: var(--muted); font-size: 0.82rem; cursor: pointer;
  padding: 0.3rem 0.65rem; border-radius: 99px; border: none; background: none; transition: all var(--transition); font-family: var(--font-body);
}
.post-action:hover { color: var(--accent2); background: rgba(108,78,242,0.1); }
.post-action.liked { color: var(--pink); }
.post-action.liked:hover { background: rgba(232,98,154,0.1); }
.post-action.bookmarked { color: var(--amber); }
.post-action.bookmarked:hover { background: rgba(245,166,35,0.1); }
.post-action .count { font-variant-numeric: tabular-nums; }
.post-more { background: none; border: none; color: var(--muted); cursor: pointer; padding: 0.35rem; border-radius: 8px; transition: all var(--transition); margin-left: auto; font-size: 1.1rem; line-height: 1; }
.post-more:hover { color: var(--text); background: var(--bg3); }

.post-menu { position: absolute; right: 1rem; top: 3.2rem; background: var(--bg3); border: 1px solid var(--border2); border-radius: var(--r); padding: 0.4rem; min-width: 170px; z-index: 20; box-shadow: 0 12px 40px rgba(0,0,0,0.5); }
.post-menu-item { display: flex; align-items: center; gap: 0.6rem; padding: 0.55rem 0.75rem; border-radius: 8px; font-size: 0.875rem; cursor: pointer; color: var(--text2); transition: background var(--transition); }
.post-menu-item:hover { background: var(--bg4); color: var(--text); }
.post-menu-item.danger { color: var(--red); }
.post-menu-item.danger:hover { background: rgba(239,68,68,0.1); }

/* ── PINNED ── */
.pinned-badge { display: inline-flex; align-items: center; gap: 0.3rem; font-size: 0.75rem; color: var(--amber); font-weight: 600; margin-bottom: 0.5rem; }

/* ── COMMENTS ── */
.comments-section { margin-top: 0.75rem; background: var(--bg2); border-radius: var(--r); overflow: hidden; border: 1px solid var(--border); }
.comment { display: flex; gap: 0.75rem; padding: 0.875rem 1rem; border-bottom: 1px solid var(--border); }
.comment:last-of-type { border-bottom: none; }
.comment-body { flex: 1; min-width: 0; }
.comment-header { display: flex; align-items: baseline; gap: 0.5rem; margin-bottom: 0.15rem; }
.comment-name { font-size: 0.875rem; font-weight: 600; cursor: pointer; }
.comment-name:hover { color: var(--accent2); }
.comment-handle { font-size: 0.78rem; color: var(--muted); }
.comment-text { font-size: 0.875rem; color: var(--text2); white-space: pre-wrap; word-break: break-word; line-height: 1.55; }
.comment-time { font-size: 0.73rem; color: var(--muted2); margin-top: 0.25rem; }
.comment-actions { display: flex; gap: 0.25rem; margin-top: 0.35rem; }
.comment-like { background: none; border: none; font-size: 0.78rem; color: var(--muted); cursor: pointer; padding: 0.2rem 0.5rem; border-radius: 99px; transition: all var(--transition); font-family: var(--font-body); display: flex; align-items: center; gap: 0.25rem; }
.comment-like:hover { background: rgba(232,98,154,0.1); color: var(--pink); }
.comment-like.liked { color: var(--pink); }
.comment-form { display: flex; gap: 0.75rem; padding: 0.875rem 1rem; align-items: center; background: var(--bg3); }
.comment-form input { flex: 1; margin-bottom: 0; }
.comment-count-label { font-size: 0.82rem; color: var(--muted); font-weight: 600; padding: 0.6rem 1rem; background: var(--bg3); border-bottom: 1px solid var(--border); }

/* ── RIGHT ASIDE ── */
.aside { padding: 1.5rem 1rem; overflow-y: auto; height: 100vh; position: sticky; top: 0; }
.widget { background: var(--bg2); border: 1px solid var(--border); border-radius: var(--r2); padding: 1.25rem; margin-bottom: 1.25rem; }
.widget-title { font-family: var(--font-head); font-size: 0.95rem; font-weight: 700; margin-bottom: 1rem; display: flex; justify-content: space-between; align-items: center; }
.widget-action { font-size: 0.8rem; color: var(--accent2); cursor: pointer; font-weight: 500; }
.widget-action:hover { text-decoration: underline; }

.trend-item { display: flex; justify-content: space-between; align-items: center; padding: 0.6rem 0; border-bottom: 1px solid var(--border); cursor: pointer; transition: all var(--transition); }
.trend-item:last-child { border-bottom: none; }
.trend-item:hover { opacity: 0.8; }
.trend-tag { font-size: 0.875rem; font-weight: 600; }
.trend-meta { font-size: 0.75rem; color: var(--muted); }
.trend-badge { background: var(--bg4); border-radius: 99px; padding: 1px 8px; font-size: 0.72rem; color: var(--muted); }

.suggest-item { display: flex; align-items: center; gap: 0.75rem; padding: 0.65rem 0; }
.suggest-info { flex: 1; min-width: 0; }
.suggest-name { font-size: 0.875rem; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.suggest-handle { font-size: 0.78rem; color: var(--muted); }
.suggest-mutual { font-size: 0.72rem; color: var(--teal); margin-top: 0.1rem; }

/* ── PROFILE ── */
.profile-cover { height: 200px; position: relative; overflow: hidden; }
.profile-cover-gradient { width: 100%; height: 100%; }
.profile-header { padding: 0 1.5rem 1.5rem; border-bottom: 1px solid var(--border); }
.profile-av-wrap { margin-top: -52px; margin-bottom: 0.875rem; }
.profile-name { font-family: var(--font-head); font-size: 1.5rem; font-weight: 800; letter-spacing: -0.02em; }
.profile-handle { color: var(--muted); font-size: 0.9rem; margin-bottom: 0.5rem; }
.profile-bio { font-size: 0.9rem; color: var(--text2); margin-bottom: 1rem; line-height: 1.6; }
.profile-meta { display: flex; gap: 1rem; flex-wrap: wrap; font-size: 0.8rem; color: var(--muted); margin-bottom: 1rem; }
.profile-meta span { display: flex; align-items: center; gap: 0.3rem; }
.profile-stats { display: flex; gap: 1.75rem; }
.stat { cursor: pointer; }
.stat:hover .stat-num { color: var(--accent2); }
.stat-num { font-family: var(--font-head); font-size: 1.25rem; font-weight: 700; transition: color var(--transition); }
.stat-label { font-size: 0.78rem; color: var(--muted); }
.profile-actions { display: flex; gap: 0.625rem; margin: 1rem 0; flex-wrap: wrap; }
.profile-tabs { display: flex; border-bottom: 1px solid var(--border); }
.profile-tab { flex: 1; padding: 0.875rem; text-align: center; font-size: 0.875rem; font-weight: 500; cursor: pointer; color: var(--muted); border: none; background: none; border-bottom: 2px solid transparent; margin-bottom: -1px; transition: all var(--transition); font-family: var(--font-body); }
.profile-tab.active { color: var(--accent2); border-bottom-color: var(--accent); }

/* ── NOTIFICATIONS ── */
.notif-item { display: flex; align-items: flex-start; gap: 0.875rem; padding: 1rem 1.5rem; border-bottom: 1px solid var(--border); transition: background var(--transition); cursor: pointer; }
.notif-item.unread { background: rgba(108,78,242,0.04); }
.notif-item:hover { background: rgba(255,255,255,0.02); }
.notif-icon { width: 36px; height: 36px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1rem; flex-shrink: 0; }
.notif-body { flex: 1; min-width: 0; }
.notif-text { font-size: 0.875rem; line-height: 1.5; color: var(--text2); }
.notif-time { font-size: 0.75rem; color: var(--muted2); margin-top: 0.2rem; }
.notif-dot { width: 7px; height: 7px; border-radius: 50%; background: var(--accent); flex-shrink: 0; margin-top: 0.5rem; }
.notif-preview { font-size: 0.8rem; color: var(--muted); margin-top: 0.25rem; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; background: var(--bg3); padding: 0.35rem 0.65rem; border-radius: 6px; }

/* ── MESSAGES ── */
.msg-layout { display: grid; grid-template-columns: 280px 1fr; height: calc(100vh - 60px); }
.msg-sidebar { border-right: 1px solid var(--border); overflow-y: auto; }
.msg-search { padding: 1rem; border-bottom: 1px solid var(--border); }
.msg-search input { margin-bottom: 0; padding: 0.6rem 1rem; }
.conv-item { display: flex; align-items: center; gap: 0.75rem; padding: 0.875rem 1rem; cursor: pointer; transition: background var(--transition); border-bottom: 1px solid var(--border); }
.conv-item:hover { background: var(--bg3); }
.conv-item.active { background: var(--bg3); }
.conv-info { flex: 1; min-width: 0; }
.conv-name { font-size: 0.875rem; font-weight: 600; }
.conv-preview { font-size: 0.78rem; color: var(--muted); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.conv-time { font-size: 0.72rem; color: var(--muted2); flex-shrink: 0; }
.conv-unread { width: 7px; height: 7px; border-radius: 50%; background: var(--accent); flex-shrink: 0; }
.msg-main { display: flex; flex-direction: column; }
.msg-header { padding: 1rem 1.25rem; border-bottom: 1px solid var(--border); display: flex; align-items: center; gap: 0.875rem; background: rgba(8,8,16,0.8); backdrop-filter: blur(12px); }
.msg-body { flex: 1; overflow-y: auto; padding: 1.25rem; display: flex; flex-direction: column; gap: 0.75rem; }
.msg-bubble-wrap { display: flex; align-items: flex-end; gap: 0.5rem; }
.msg-bubble-wrap.mine { flex-direction: row-reverse; }
.msg-bubble { max-width: 72%; padding: 0.65rem 1rem; border-radius: 18px; font-size: 0.9rem; line-height: 1.55; position: relative; }
.msg-bubble.them { background: var(--bg3); border-bottom-left-radius: 4px; }
.msg-bubble.mine { background: var(--accent); color: white; border-bottom-right-radius: 4px; box-shadow: 0 2px 12px var(--glow); }
.msg-bubble-time { font-size: 0.7rem; color: var(--muted2); margin-top: 0.2rem; text-align: right; }
.msg-footer { padding: 1rem 1.25rem; border-top: 1px solid var(--border); display: flex; gap: 0.75rem; align-items: center; }
.msg-footer input { flex: 1; margin-bottom: 0; }
.msg-empty { display: flex; align-items: center; justify-content: center; flex: 1; color: var(--muted); flex-direction: column; gap: 1rem; font-size: 0.9rem; }

/* ── SEARCH ── */
.search-input-wrap { position: relative; padding: 1rem 1.5rem; border-bottom: 1px solid var(--border); }
.search-input-wrap input { padding-left: 2.5rem; margin-bottom: 0; }
.search-icon { position: absolute; left: 2.25rem; top: 50%; transform: translateY(-50%); color: var(--muted); pointer-events: none; }
.search-filter-tabs { display: flex; gap: 0.5rem; padding: 0.75rem 1.5rem; border-bottom: 1px solid var(--border); overflow-x: auto; }
.filter-chip { padding: 0.35rem 0.85rem; border-radius: 99px; font-size: 0.82rem; cursor: pointer; border: 1px solid var(--border2); background: transparent; color: var(--muted); transition: all var(--transition); font-family: var(--font-body); white-space: nowrap; }
.filter-chip.active { border-color: var(--accent); background: rgba(108,78,242,0.15); color: var(--accent3); }

/* ── EMPTY STATE ── */
.empty-state { text-align: center; padding: 4rem 2rem; color: var(--muted); }
.es-icon { font-size: 2.5rem; margin-bottom: 0.875rem; opacity: 0.35; }
.empty-state h3 { font-family: var(--font-head); font-size: 1.1rem; color: var(--text); margin-bottom: 0.5rem; }
.empty-state p { font-size: 0.875rem; line-height: 1.6; }

/* ── MODAL ── */
.modal-overlay { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.7); backdrop-filter: blur(6px); z-index: 100; align-items: center; justify-content: center; }
.modal-overlay.open { display: flex; }
.modal { background: var(--bg2); border: 1px solid var(--border2); border-radius: var(--r3); padding: 2rem; width: 500px; max-width: calc(100vw - 2rem); max-height: 88vh; overflow-y: auto; box-shadow: 0 32px 80px rgba(0,0,0,0.6); animation: modalIn 0.25s cubic-bezier(0.16,1,0.3,1); }
@keyframes modalIn { from { opacity:0; transform: scale(0.95) translateY(10px); } to { opacity:1; transform:none; } }
.modal-title { font-family: var(--font-head); font-size: 1.2rem; font-weight: 700; margin-bottom: 1.5rem; display: flex; justify-content: space-between; align-items: center; }
.modal-close { background: none; border: none; color: var(--muted); cursor: pointer; font-size: 1.4rem; padding: 0.2rem 0.4rem; border-radius: 6px; transition: all var(--transition); line-height: 1; }
.modal-close:hover { color: var(--text); background: var(--bg4); }

/* Poll builder */
.poll-builder { margin-bottom: 1rem; }
.poll-opt-row { display: flex; gap: 0.5rem; margin-bottom: 0.5rem; align-items: center; }
.poll-opt-row input { margin-bottom: 0; flex: 1; }
.poll-opt-row button { background: none; border: 1px solid var(--border); border-radius: 8px; color: var(--muted); cursor: pointer; padding: 0.4rem 0.6rem; font-size: 0.85rem; transition: all var(--transition); }
.poll-opt-row button:hover { border-color: var(--red); color: var(--red); }

/* ── TOAST ── */
.toast-wrap { position: fixed; bottom: 1.5rem; right: 1.5rem; z-index: 200; display: flex; flex-direction: column; gap: 0.4rem; }
.toast { background: var(--bg3); border: 1px solid var(--border2); border-radius: var(--r); padding: 0.8rem 1.25rem; font-size: 0.875rem; display: flex; align-items: center; gap: 0.6rem; animation: toastIn 0.3s cubic-bezier(0.16,1,0.3,1); box-shadow: 0 8px 32px rgba(0,0,0,0.4); min-width: 240px; backdrop-filter: blur(12px); }
@keyframes toastIn { from { opacity:0; transform: translateX(20px); } to { opacity:1; transform:none; } }
.toast.fadeOut { animation: toastOut 0.3s ease forwards; }
@keyframes toastOut { to { opacity:0; transform: translateX(20px); } }
.toast-icon { font-size: 1rem; flex-shrink: 0; }
.toast.success { border-color: rgba(34,197,94,0.25); }
.toast.success .toast-icon { color: var(--green); }
.toast.error { border-color: rgba(239,68,68,0.25); }
.toast.error .toast-icon { color: var(--red); }
.toast.info .toast-icon { color: var(--accent2); }

/* ── PAGES ── */
.page { display: none; }
.page.active { display: block; }

/* ── LOADING SPINNER ── */
.spinner { width: 20px; height: 20px; border: 2px solid var(--border2); border-top-color: var(--accent); border-radius: 50%; animation: spin 0.6s linear infinite; margin: 2rem auto; }
@keyframes spin { to { transform: rotate(360deg); } }

/* ── MEDIA GRID ── */
.media-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 4px; border-radius: var(--r); overflow: hidden; margin-bottom: 0.875rem; }
.media-grid img { width: 100%; height: 160px; object-fit: cover; display: block; }
.media-grid img:only-child { grid-column: 1/-1; height: 280px; }

/* ── PROGRESS RING ── */
.progress-ring-wrap { position: relative; width: 36px; height: 36px; flex-shrink: 0; }
.progress-ring { transform: rotate(-90deg); }
.progress-ring circle { transition: stroke-dashoffset 0.3s ease; }

/* ── LINK PREVIEW ── */
.link-preview { border: 1px solid var(--border); border-radius: var(--r); overflow: hidden; margin-bottom: 0.875rem; display: flex; }
.link-preview-img { width: 80px; background: var(--bg4); display: flex; align-items: center; justify-content: center; font-size: 2rem; flex-shrink: 0; }
.link-preview-body { padding: 0.75rem; flex: 1; min-width: 0; }
.link-preview-domain { font-size: 0.72rem; color: var(--muted); margin-bottom: 0.2rem; }
.link-preview-title { font-size: 0.875rem; font-weight: 600; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }

/* ── FOLLOWER MODAL ── */
.follow-list-item { display: flex; align-items: center; gap: 0.75rem; padding: 0.75rem 0; border-bottom: 1px solid var(--border); }
.follow-list-item:last-child { border-bottom: none; }

/* Responsive */
@media (max-width: 1100px) { .layout { grid-template-columns: var(--sidebar-w) 1fr; } .aside { display: none; } }
@media (max-width: 700px) { .layout { grid-template-columns: 1fr; } .sidebar { display: none; } }
</style>
</head>
<body>

<!-- ════ AUTH ════ -->
<div id="auth-screen">
  <div class="auth-orbs"><div class="auth-orb"></div><div class="auth-orb"></div><div class="auth-orb"></div></div>
  <div class="auth-box">
    <div class="auth-logo">Nexus<span class="logo-dot">.</span></div>
    <p class="auth-sub">Ton espace, ta communauté, tes règles.</p>
    <div class="auth-tabs">
      <button class="auth-tab active" onclick="showAuthTab('login')">Connexion</button>
      <button class="auth-tab" onclick="showAuthTab('register')">Inscription</button>
    </div>
    <!-- Login -->
    <div id="tab-login">
      <div class="auth-err" id="login-err">Email ou mot de passe incorrect.</div>
      <label>Email</label>
      <input type="email" id="login-email" placeholder="toi@exemple.com" onkeydown="if(event.key==='Enter')doLogin()">
      <label>Mot de passe</label>
      <input type="password" id="login-pass" placeholder="••••••••" onkeydown="if(event.key==='Enter')doLogin()">
      <button class="btn btn-primary" onclick="doLogin()">Se connecter →</button>
    </div>
    <!-- Register -->
    <div id="tab-register" style="display:none">
      <div class="auth-err" id="reg-err"></div>
      <label>Nom complet</label>
      <input type="text" id="reg-name" placeholder="Marie Dupont">
      <label>Nom d'utilisateur</label>
      <input type="text" id="reg-handle" placeholder="marie">
      <label>Email</label>
      <input type="email" id="reg-email" placeholder="marie@exemple.com">
      <label>Mot de passe</label>
      <input type="password" id="reg-pass" placeholder="Min. 6 caractères">
      <label>Avatar</label>
      <div class="av-pick" id="avatar-pick"></div>
      <button class="btn btn-primary" onclick="doRegister()">Créer mon compte →</button>
    </div>
  </div>
</div>

<!-- ════ APP ════ -->
<div id="app">
  <div class="layout">

    <!-- SIDEBAR -->
    <nav class="sidebar">
      <div class="logo" onclick="gotoPage('feed',null);document.querySelectorAll('.nav-item').forEach(b=>b.classList.remove('active'));document.querySelector('.nav-item').classList.add('active')">Nexus<span class="logo-dot">.</span></div>
      <button class="nav-item active" onclick="gotoPage('feed',this)"><span class="nav-icon">🏠</span><span class="nav-label">Fil d'actualité</span></button>
      <button class="nav-item" onclick="gotoPage('explore',this)"><span class="nav-icon">🔍</span><span class="nav-label">Explorer</span></button>
      <button class="nav-item" onclick="gotoPage('messages',this)"><span class="nav-icon">✉️</span><span class="nav-label">Messages</span><span class="nav-badge" id="msg-badge" style="display:none">0</span></button>
      <button class="nav-item" onclick="gotoPage('notifications',this)"><span class="nav-icon">🔔</span><span class="nav-label">Notifications</span><span class="nav-badge" id="notif-badge" style="display:none">0</span></button>
      <button class="nav-item" onclick="gotoPage('bookmarks',this)"><span class="nav-icon">🔖</span><span class="nav-label">Signets</span></button>
      <div class="sidebar-divider"></div>
      <button class="nav-item" onclick="gotoOwnProfile()"><span class="nav-icon">👤</span><span class="nav-label">Mon profil</span></button>
      <button class="nav-item" onclick="openEditProfile()"><span class="nav-icon">⚙️</span><span class="nav-label">Paramètres</span></button>
      <div class="sidebar-user" onclick="gotoOwnProfile()">
        <div class="avatar sz-sm" id="sidebar-av"></div>
        <div style="flex:1;overflow:hidden">
          <div style="font-size:0.875rem;font-weight:600;white-space:nowrap;overflow:hidden;text-overflow:ellipsis" id="sidebar-name"></div>
          <div style="font-size:0.75rem;color:var(--muted)" id="sidebar-handle"></div>
        </div>
        <button class="btn btn-ghost btn-sm" onclick="doLogout(event)" title="Déconnexion">↩</button>
      </div>
    </nav>

    <!-- MAIN -->
    <main class="feed">

      <!-- FEED -->
      <div class="page active" id="page-feed">
        <div class="feed-header">
          <div class="feed-title">Accueil</div>
          <button class="btn btn-ghost btn-sm" onclick="renderFeed();toast('Actualisé !','info')">↺ Actualiser</button>
        </div>
        <div class="feed-tabs">
          <button class="feed-tab active" onclick="switchFeedTab('all',this)">Tout</button>
          <button class="feed-tab" onclick="switchFeedTab('following',this)">Abonnements</button>
          <button class="feed-tab" onclick="switchFeedTab('media',this)">Médias</button>
        </div>
        <div class="compose">
          <div class="avatar sz-md" id="compose-av" onclick="gotoOwnProfile()"></div>
          <div class="compose-area">
            <div class="mood-bar" id="mood-bar"></div>
            <textarea id="compose-text" placeholder="Quoi de neuf ?" oninput="updateCharCount()" maxlength="500"></textarea>
            <div id="img-preview" style="display:none;position:relative;margin-bottom:0.75rem">
              <img id="img-prev-img" style="width:100%;border-radius:var(--r);max-height:200px;object-fit:cover">
              <button onclick="clearImage()" style="position:absolute;top:6px;right:6px;background:rgba(0,0,0,0.75);border:none;color:white;border-radius:50%;width:28px;height:28px;cursor:pointer;font-size:0.85rem;line-height:1">✕</button>
            </div>
            <div id="poll-preview" style="display:none" class="poll-builder"></div>
            <div class="compose-footer">
              <div class="compose-tools">
                <button class="compose-tool" title="Ajouter une image" onclick="document.getElementById('img-upload').click()">🖼️</button>
                <button class="compose-tool" title="Ajouter un sondage" onclick="togglePollBuilder()">📊</button>
                <button class="compose-tool" title="Hashtag" onclick="insertHashtag()">#</button>
                <button class="compose-tool" title="Humeur" onclick="toggleMoodPicker()">😊</button>
              </div>
              <div style="display:flex;align-items:center;gap:0.75rem">
                <div style="position:relative;width:36px;height:36px">
                  <svg class="progress-ring" width="36" height="36" viewBox="0 0 36 36">
                    <circle stroke="var(--bg5)" stroke-width="3" fill="none" cx="18" cy="18" r="15"/>
                    <circle id="char-ring" stroke="var(--accent)" stroke-width="3" fill="none" cx="18" cy="18" r="15"
                      stroke-dasharray="94.25" stroke-dashoffset="94.25" stroke-linecap="round"/>
                  </svg>
                  <span id="char-count" style="position:absolute;inset:0;display:flex;align-items:center;justify-content:center;font-size:0.68rem;color:var(--muted)"></span>
                </div>
                <button class="btn btn-primary btn-sm" onclick="submitPost()">Publier</button>
              </div>
            </div>
            <input type="file" id="img-upload" accept="image/*" style="display:none" onchange="handleImageUpload(event)">
          </div>
        </div>
        <div id="feed-posts"></div>
      </div>

      <!-- EXPLORE -->
      <div class="page" id="page-explore">
        <div class="feed-header"><div class="feed-title">Explorer</div></div>
        <div class="search-input-wrap">
          <span class="search-icon">🔍</span>
          <input type="text" id="search-q" placeholder="Rechercher des personnes, posts, hashtags…" oninput="doSearch()">
        </div>
        <div class="search-filter-tabs" id="search-filters">
          <button class="filter-chip active" onclick="setSearchFilter('all',this)">Tout</button>
          <button class="filter-chip" onclick="setSearchFilter('users',this)">Personnes</button>
          <button class="filter-chip" onclick="setSearchFilter('posts',this)">Posts</button>
          <button class="filter-chip" onclick="setSearchFilter('tags',this)">Hashtags</button>
        </div>
        <div id="search-results">
          <div style="padding:1.5rem 1.5rem 0.5rem;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--muted);font-weight:600">Tendances du moment</div>
          <div id="explore-trends"></div>
        </div>
      </div>

      <!-- MESSAGES -->
      <div class="page" id="page-messages">
        <div class="feed-header"><div class="feed-title">Messages</div><button class="btn btn-ghost btn-sm" onclick="openNewMsg()">+ Nouveau</button></div>
        <div class="msg-layout">
          <div class="msg-sidebar">
            <div class="msg-search"><input type="text" placeholder="Rechercher…" oninput="filterConvs(this.value)" id="conv-search"></div>
            <div id="conv-list"></div>
          </div>
          <div class="msg-main" id="msg-main">
            <div class="msg-empty"><div style="font-size:2.5rem;opacity:0.3">✉️</div><span>Sélectionne une conversation</span></div>
          </div>
        </div>
      </div>

      <!-- NOTIFICATIONS -->
      <div class="page" id="page-notifications">
        <div class="feed-header">
          <div class="feed-title">Notifications</div>
          <button class="btn btn-ghost btn-sm" onclick="markAllRead()">Tout marquer lu</button>
        </div>
        <div id="notif-list"></div>
      </div>

      <!-- BOOKMARKS -->
      <div class="page" id="page-bookmarks">
        <div class="feed-header"><div class="feed-title">Signets</div><button class="btn btn-danger btn-sm" onclick="clearBookmarks()">Tout effacer</button></div>
        <div id="bookmark-posts"></div>
      </div>

      <!-- PROFILE -->
      <div class="page" id="page-profile">
        <div class="profile-cover"><canvas id="profile-cover" width="800" height="200"></canvas></div>
        <div class="profile-header">
          <div class="profile-av-wrap"><div class="avatar sz-xxl" id="profile-av"></div></div>
          <div id="profile-actions" class="profile-actions"></div>
          <div class="profile-name" id="profile-name"></div>
          <div class="profile-handle" id="profile-handle"></div>
          <div class="profile-bio" id="profile-bio"></div>
          <div class="profile-meta" id="profile-meta"></div>
          <div class="profile-stats">
            <div class="stat" onclick="showFollowModal('posts')"><div class="stat-num" id="p-posts">0</div><div class="stat-label">Posts</div></div>
            <div class="stat" onclick="showFollowModal('followers')"><div class="stat-num" id="p-followers">0</div><div class="stat-label">Abonnés</div></div>
            <div class="stat" onclick="showFollowModal('following')"><div class="stat-num" id="p-following">0</div><div class="stat-label">Abonnements</div></div>
          </div>
        </div>
        <div class="profile-tabs">
          <button class="profile-tab active" onclick="switchProfileTab('posts',this)">Posts</button>
          <button class="profile-tab" onclick="switchProfileTab('replies',this)">Réponses</button>
          <button class="profile-tab" onclick="switchProfileTab('media',this)">Médias</button>
          <button class="profile-tab" onclick="switchProfileTab('likes',this)">J'aime</button>
        </div>
        <div id="profile-posts"></div>
      </div>

    </main>

    <!-- RIGHT ASIDE -->
    <aside class="aside">
      <div class="widget">
        <div class="widget-title">Tendances <span class="widget-action" onclick="gotoPage('explore',document.querySelectorAll('.nav-item')[1])">Voir tout →</span></div>
        <div id="trends-list"></div>
      </div>
      <div class="widget">
        <div class="widget-title">Suggestions <span class="widget-action" onclick="renderSuggestions(true)">Actualiser</span></div>
        <div id="suggest-list"></div>
      </div>
      <div class="widget" id="active-poll-widget" style="display:none">
        <div class="widget-title">Sondage actif</div>
        <div id="active-poll-content"></div>
      </div>
    </aside>
  </div>
</div>

<!-- TOAST -->
<div class="toast-wrap" id="toast-wrap"></div>

<!-- EDIT PROFILE MODAL -->
<div class="modal-overlay" id="modal-editprofile">
  <div class="modal">
    <div class="modal-title">Modifier le profil <button class="modal-close" onclick="closeModal('modal-editprofile')">✕</button></div>
    <label>Nom complet</label><input type="text" id="ep-name">
    <label>Nom d'utilisateur</label><input type="text" id="ep-handle">
    <label>Site web / Lien</label><input type="text" id="ep-website" placeholder="https://monsite.com">
    <label>Localisation</label><input type="text" id="ep-location" placeholder="Paris, France">
    <label>Biographie</label><textarea id="ep-bio" style="min-height:80px;resize:none"></textarea>
    <label>Avatar</label>
    <div class="av-pick" id="ep-avatar-pick"></div>
    <button class="btn btn-primary" onclick="saveProfile()">Enregistrer</button>
  </div>
</div>

<!-- FOLLOWERS MODAL -->
<div class="modal-overlay" id="modal-follows">
  <div class="modal">
    <div class="modal-title" id="follow-modal-title">Abonnés <button class="modal-close" onclick="closeModal('modal-follows')">✕</button></div>
    <div id="follow-list"></div>
  </div>
</div>

<!-- NEW MESSAGE MODAL -->
<div class="modal-overlay" id="modal-newmsg">
  <div class="modal">
    <div class="modal-title">Nouveau message <button class="modal-close" onclick="closeModal('modal-newmsg')">✕</button></div>
    <label>Envoyer à</label>
    <input type="text" id="newmsg-search" placeholder="Rechercher un utilisateur…" oninput="searchForMsg()">
    <div id="newmsg-results"></div>
  </div>
</div>

<script>
// ════════════════════════════════════════
// DATA & STATE
// ════════════════════════════════════════
const AV_EMOJIS = ['🦊','🐺','🦁','🐯','🐻','🦄','🐸','🦋','🐬','🦅','🌻','🌙','🦚','🦜','🐙','🦩'];
const AV_COLORS = ['#2d1f5e','#1f3a5e','#1f5e3a','#5e3a1f','#5e1f3a','#1f4a5e','#3d3d1f','#5e1f5e','#1f5e5e','#4a1f1f','#2a4a2a','#1a1a4a','#3a1a4a','#4a2a1a','#1a3a3a','#3a1a2a'];
const MOODS = ['😊 Heureux','😎 Détendu','🤔 Pensif','🔥 Motivé','💡 Inspiré','😴 Fatigué','🎉 Fêtard','❤️ Amoureux'];

function LS(k, d) { try { const v = localStorage.getItem(k); return v !== null ? JSON.parse(v) : d; } catch { return d; } }
function LSset(k, v) { try { localStorage.setItem(k, JSON.stringify(v)); } catch(e) { console.warn('Storage full'); } }

let currentUser = null;
let currentProfileId = null;
let selectedAvatar = { emoji: AV_EMOJIS[0], color: AV_COLORS[0] };
let selectedAvatarEdit = null;
let pendingImage = null;
let pendingPoll = null;
let pendingMood = null;
let feedTab = 'all';
let openMenuId = null;
let activeConvId = null;
let searchFilter = 'all';
let profileTab = 'posts';

// ════════════════════════════════════════
// AUTH
// ════════════════════════════════════════
function showAuthTab(t) {
  document.querySelectorAll('.auth-tab').forEach((b, i) => b.classList.toggle('active', (t==='login'&&i===0)||(t==='register'&&i===1)));
  document.getElementById('tab-login').style.display = t==='login' ? '' : 'none';
  document.getElementById('tab-register').style.display = t==='register' ? '' : 'none';
}

function buildAvatarPick(containerId, onPickFn) {
  const el = document.getElementById(containerId);
  if (!el) return;
  el.innerHTML = AV_EMOJIS.map((e, i) => `<div class="av-opt" data-idx="${i}" style="background:${AV_COLORS[i]}" onclick="${onPickFn}(this)">${e}</div>`).join('');
}

function pickAvatar(el) {
  document.querySelectorAll('#avatar-pick .av-opt').forEach(x => x.classList.remove('selected'));
  el.classList.add('selected');
  const idx = parseInt(el.dataset.idx);
  selectedAvatar = { emoji: AV_EMOJIS[idx], color: AV_COLORS[idx] };
}

function pickAvatarEdit(el) {
  document.querySelectorAll('#ep-avatar-pick .av-opt').forEach(x => x.classList.remove('selected'));
  el.classList.add('selected');
  const idx = parseInt(el.dataset.idx);
  selectedAvatarEdit = { emoji: AV_EMOJIS[idx], color: AV_COLORS[idx] };
}

function doLogin() {
  const email = document.getElementById('login-email').value.trim();
  const pass = document.getElementById('login-pass').value;
  const errEl = document.getElementById('login-err');
  const users = LS('nx_users', []);
  const user = users.find(u => u.email === email && u.password === pass);
  if (!user) { errEl.classList.add('show'); return; }
  errEl.classList.remove('show');
  LSset('nx_session', user.id);
  currentUser = user;
  launchApp();
}

function doRegister() {
  const name = document.getElementById('reg-name').value.trim();
  const handle = document.getElementById('reg-handle').value.trim().replace('@', '').replace(/\s/g,'');
  const email = document.getElementById('reg-email').value.trim();
  const pass = document.getElementById('reg-pass').value;
  const errEl = document.getElementById('reg-err');
  const showErr = msg => { errEl.textContent = msg; errEl.classList.add('show'); };
  const users = LS('nx_users', []);
  if (!name || !handle || !email || !pass) return showErr('Tous les champs sont requis.');
  if (pass.length < 6) return showErr('Mot de passe trop court (6 caractères minimum).');
  if (!/^[a-zA-Z0-9_]+$/.test(handle)) return showErr('Nom d\'utilisateur : lettres, chiffres et _ uniquement.');
  if (users.find(u => u.email === email)) return showErr('Email déjà utilisé.');
  if (users.find(u => u.handle.toLowerCase() === handle.toLowerCase())) return showErr('Nom d\'utilisateur déjà pris.');
  errEl.classList.remove('show');
  const user = {
    id: Date.now().toString(), name, handle: handle.toLowerCase(), email, password: pass,
    avatar: selectedAvatar.emoji, avatarColor: selectedAvatar.color,
    bio: '', website: '', location: '', followers: [], following: [],
    pinnedPost: null, createdAt: Date.now()
  };
  users.push(user);
  LSset('nx_users', users);
  LSset('nx_session', user.id);
  currentUser = user;
  launchApp();
  toast(`Bienvenue sur Nexus, @${user.handle} ! 🎉`, 'success');
}

function doLogout(e) {
  e && e.stopPropagation();
  localStorage.removeItem('nx_session');
  currentUser = null;
  document.getElementById('app').style.display = 'none';
  document.getElementById('auth-screen').style.display = 'flex';
  toast('À bientôt ! 👋', 'info');
}

// ════════════════════════════════════════
// APP INIT
// ════════════════════════════════════════
function launchApp() {
  document.getElementById('auth-screen').style.display = 'none';
  document.getElementById('app').style.display = 'block';
  refreshCurrentUser();
  updateSidebar();
  renderFeed();
  renderTrends();
  renderSuggestions();
  updateNotifBadge();
  renderMoodBar();
  gotoPage('feed', document.querySelector('.nav-item'));
}

function refreshCurrentUser() {
  const users = LS('nx_users', []);
  currentUser = users.find(u => u.id === currentUser.id) || currentUser;
}

function updateSidebar() {
  const av = document.getElementById('sidebar-av');
  av.textContent = currentUser.avatar;
  av.style.background = currentUser.avatarColor;
  document.getElementById('sidebar-name').textContent = currentUser.name;
  document.getElementById('sidebar-handle').textContent = '@' + currentUser.handle;
  const cav = document.getElementById('compose-av');
  cav.textContent = currentUser.avatar;
  cav.style.background = currentUser.avatarColor;
}

// ════════════════════════════════════════
// NAVIGATION
// ════════════════════════════════════════
function gotoPage(id, btn) {
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-' + id).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('active'));
  if (btn) btn.classList.add('active');
  if (id === 'feed') renderFeed();
  else if (id === 'notifications') { renderNotifications(); markAllRead(); }
  else if (id === 'bookmarks') renderBookmarks();
  else if (id === 'explore') renderExploreTrends();
  else if (id === 'messages') renderConvList();
}

function gotoOwnProfile() {
  currentProfileId = currentUser.id;
  profileTab = 'posts';
  renderProfile(currentUser.id);
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-profile').classList.add('active');
  document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('active'));
}

function gotoProfile(uid) {
  currentProfileId = uid;
  profileTab = 'posts';
  renderProfile(uid);
  document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
  document.getElementById('page-profile').classList.add('active');
  document.querySelectorAll('.nav-item').forEach(b => b.classList.remove('active'));
}

// ════════════════════════════════════════
// FEED
// ════════════════════════════════════════
function switchFeedTab(tab, btn) {
  feedTab = tab;
  document.querySelectorAll('.feed-tab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderFeed();
}

function renderFeed() {
  let posts = LS('nx_posts', []).sort((a, b) => b.createdAt - a.createdAt);
  if (feedTab === 'following') posts = posts.filter(p => (currentUser.following || []).includes(p.userId) || p.userId === currentUser.id);
  else if (feedTab === 'media') posts = posts.filter(p => p.image);
  const el = document.getElementById('feed-posts');
  if (!posts.length) {
    el.innerHTML = `<div class="empty-state"><div class="es-icon">📭</div><h3>Rien à afficher</h3><p>${feedTab === 'following' ? 'Abonne-toi à des utilisateurs pour voir leurs posts.' : 'Sois le premier à publier quelque chose !'}</p></div>`;
    return;
  }
  el.innerHTML = posts.map(p => renderPostCard(p)).join('');
}

// ════════════════════════════════════════
// POST CARD
// ════════════════════════════════════════
function renderPostCard(post, opts = {}) {
  const users = LS('nx_users', []);
  const author = users.find(u => u.id === post.userId) || { name: 'Utilisateur', handle: 'deleted', avatar: '❓', avatarColor: '#333', id: '' };
  const liked = (post.likes || []).includes(currentUser.id);
  const bm = isBookmarked(post.id);
  const comments = LS('nx_comments_' + post.id, []);
  const isOwn = post.userId === currentUser.id;
  const tags = (post.tags || []).map(t => `<span class="post-tag" onclick="searchByTag('${esc(t)}')">#${esc(t)}</span>`).join('');
  const moodHtml = post.mood ? `<div class="post-mood">${post.mood}</div>` : '';
  const pinnedHtml = isOwn && author.pinnedPost === post.id ? `<div class="pinned-badge">📌 Post épinglé</div>` : '';
  const imgHtml = post.image ? `<img class="post-image" src="${post.image}" alt="photo" loading="lazy">` : '';

  // Render body with @mention highlighting
  const bodyHtml = esc(post.text).replace(/@([a-zA-Z0-9_]+)/g, (m, h) => {
    const u = users.find(x => x.handle === h.toLowerCase());
    return u ? `<span class="mention" onclick="gotoProfile('${u.id}')">@${h}</span>` : m;
  });

  // Poll
  let pollHtml = '';
  if (post.poll) {
    const total = post.poll.options.reduce((s, o) => s + (o.votes || []).length, 0);
    const myVote = post.poll.options.findIndex(o => (o.votes || []).includes(currentUser.id));
    const hasVoted = myVote > -1;
    pollHtml = `<div class="poll">
      ${post.poll.options.map((o, i) => {
        const votes = (o.votes || []).length;
        const pct = total ? Math.round(votes / total * 100) : 0;
        const isWin = hasVoted && votes === Math.max(...post.poll.options.map(x => (x.votes||[]).length));
        return `<div class="poll-option ${hasVoted ? 'voted' : ''} ${isWin ? 'winner' : ''}" onclick="votePoll('${post.id}',${i})">
          <div class="poll-bar" style="width:${hasVoted ? pct : 0}%"></div>
          <span class="poll-label">${esc(o.text)}</span>
          ${hasVoted ? `<span class="poll-pct">${pct}%</span>` : ''}
          ${myVote === i ? ' ✓' : ''}
        </div>`;
      }).join('')}
      <div class="poll-info">${total} vote${total!==1?'s':''} · ${post.poll.endsIn || 'Ouvert'}</div>
    </div>`;
  }

  const menuItems = isOwn
    ? `<div class="post-menu-item" onclick="pinPost('${post.id}')">📌 ${author.pinnedPost===post.id?'Désépingler':'Épingler'}</div>
       <div class="post-menu-item danger" onclick="deletePost('${post.id}')">🗑️ Supprimer</div>`
    : `<div class="post-menu-item" onclick="startMsgWithUser('${author.id}')">✉️ Envoyer un message</div>
       <div class="post-menu-item" onclick="reportPost('${post.id}')">🚩 Signaler</div>`;

  const commentsHtml = opts.showComments ? renderComments(post.id) : '';

  return `<div class="post-wrap">
    <div class="post" id="post-${post.id}">
      ${pinnedHtml}
      <div class="post-header">
        <div class="avatar sz-md" style="background:${esc(author.avatarColor)}" onclick="gotoProfile('${esc(author.id)}')">${author.avatar}</div>
        <div class="post-meta">
          <div>
            <span class="post-name" onclick="gotoProfile('${esc(author.id)}')">${esc(author.name)}</span>
            <span class="post-handle"> · @${esc(author.handle)}</span>
          </div>
          <div class="post-time">${timeAgo(post.createdAt)}</div>
          ${moodHtml}
        </div>
        <button class="post-more" onclick="toggleMenu('${post.id}',event)">⋯</button>
      </div>
      <div class="post-body">${bodyHtml}</div>
      ${tags}
      ${imgHtml}
      ${pollHtml}
      <div class="post-actions">
        <button class="post-action ${liked ? 'liked' : ''}" onclick="toggleLike('${post.id}')">
          ${liked ? '❤️' : '🤍'} <span class="count">${(post.likes || []).length}</span>
        </button>
        <button class="post-action" onclick="toggleComments('${post.id}')">
          💬 <span class="count">${comments.length}</span>
        </button>
        <button class="post-action" onclick="repost('${post.id}')">🔁 <span class="count">${post.reposts||0}</span></button>
        <button class="post-action ${bm ? 'bookmarked' : ''}" onclick="toggleBookmark('${post.id}')">
          ${bm ? '🔖' : '🏷️'}
        </button>
        <button class="post-action" onclick="sharePost('${post.id}')">🔗</button>
      </div>
      ${commentsHtml}
    </div>
    <div class="post-menu" id="menu-${post.id}" style="display:none">
      <div class="post-menu-item" onclick="sharePost('${post.id}')">🔗 Copier le lien</div>
      ${menuItems}
    </div>
  </div>`;
}

function renderComments(postId) {
  const users = LS('nx_users', []);
  const comments = LS('nx_comments_' + postId, []);
  return `<div class="comments-section">
    ${comments.length ? `<div class="comment-count-label">${comments.length} commentaire${comments.length>1?'s':''}</div>` : ''}
    ${comments.map(c => {
      const cu = users.find(u => u.id === c.userId) || { name:'?', avatar:'❓', avatarColor:'#333', id:'' };
      const cLiked = (c.likes || []).includes(currentUser.id);
      return `<div class="comment">
        <div class="avatar sz-sm" style="background:${esc(cu.avatarColor)}" onclick="gotoProfile('${esc(cu.id)}')">${cu.avatar}</div>
        <div class="comment-body">
          <div class="comment-header">
            <span class="comment-name" onclick="gotoProfile('${esc(cu.id)}')">${esc(cu.name)}</span>
            <span class="comment-handle">@${esc(cu.handle)}</span>
          </div>
          <div class="comment-text">${esc(c.text)}</div>
          <div class="comment-time">${timeAgo(c.createdAt)}</div>
          <div class="comment-actions">
            <button class="comment-like ${cLiked?'liked':''}" onclick="likeComment('${postId}','${c.id}')">
              ${cLiked?'❤️':'🤍'} ${(c.likes||[]).length||''}
            </button>
          </div>
        </div>
      </div>`;
    }).join('')}
    <div class="comment-form">
      <div class="avatar sz-sm" style="background:${esc(currentUser.avatarColor)}">${currentUser.avatar}</div>
      <input type="text" id="cmt-${postId}" placeholder="Écrire un commentaire…" onkeydown="if(event.key==='Enter')addComment('${postId}')">
      <button class="btn btn-ghost btn-sm" onclick="addComment('${postId}')">Envoyer</button>
    </div>
  </div>`;
}

// ════════════════════════════════════════
// COMPOSE
// ════════════════════════════════════════
function renderMoodBar() {
  const bar = document.getElementById('mood-bar');
  if (!bar) return;
  bar.innerHTML = MOODS.map(m => `<button class="mood-chip" onclick="selectMood('${m}',this)">${m}</button>`).join('');
}

function toggleMoodPicker() {
  const bar = document.getElementById('mood-bar');
  bar.style.display = bar.style.display === 'none' ? '' : 'none';
}

function selectMood(m, el) {
  pendingMood = pendingMood === m ? null : m;
  document.querySelectorAll('.mood-chip').forEach(c => c.classList.remove('selected'));
  if (pendingMood) el.classList.add('selected');
}

function updateCharCount() {
  const v = document.getElementById('compose-text').value.length;
  const max = 500;
  const rem = max - v;
  const pct = v / max;
  const circ = 94.25;
  const offset = circ - pct * circ;
  const ring = document.getElementById('char-ring');
  if (ring) {
    ring.style.strokeDashoffset = offset;
    ring.style.stroke = rem < 50 ? (rem < 20 ? '#ef4444' : '#f5a623') : 'var(--accent)';
  }
  const cnt = document.getElementById('char-count');
  if (cnt) cnt.textContent = rem < 100 ? rem : '';
}

function insertHashtag() {
  const ta = document.getElementById('compose-text');
  const pos = ta.selectionStart;
  const before = ta.value.substring(0, pos);
  const after = ta.value.substring(pos);
  const insert = (before.length && !before.endsWith(' ')) ? ' #' : '#';
  ta.value = before + insert + after;
  ta.selectionStart = ta.selectionEnd = pos + insert.length;
  ta.focus();
  updateCharCount();
}

function handleImageUpload(e) {
  const file = e.target.files[0];
  if (!file) return;
  if (file.size > 5 * 1024 * 1024) { toast('Image trop lourde (max 5 Mo)', 'error'); return; }
  const reader = new FileReader();
  reader.onload = ev => {
    pendingImage = ev.target.result;
    document.getElementById('img-prev-img').src = pendingImage;
    document.getElementById('img-preview').style.display = 'block';
  };
  reader.readAsDataURL(file);
}

function clearImage() {
  pendingImage = null;
  document.getElementById('img-preview').style.display = 'none';
  document.getElementById('img-upload').value = '';
}

// Poll builder
let pollOptions = ['', ''];

function togglePollBuilder() {
  const div = document.getElementById('poll-preview');
  if (div.style.display === 'none') {
    pendingPoll = { options: ['', ''] };
    pollOptions = ['', ''];
    div.style.display = '';
    renderPollBuilder();
  } else {
    div.style.display = 'none';
    pendingPoll = null;
    pollOptions = ['', ''];
  }
}

function renderPollBuilder() {
  const div = document.getElementById('poll-preview');
  div.innerHTML = `<div style="margin-bottom:0.5rem;font-size:0.82rem;font-weight:600;color:var(--muted);text-transform:uppercase;letter-spacing:0.07em">Options du sondage</div>
    ${pollOptions.map((o, i) => `<div class="poll-opt-row">
      <input type="text" value="${esc(o)}" placeholder="Option ${i+1}" oninput="pollOptions[${i}]=this.value" maxlength="80">
      ${pollOptions.length > 2 ? `<button onclick="removePollOpt(${i})">✕</button>` : ''}
    </div>`).join('')}
    ${pollOptions.length < 4 ? `<button class="btn btn-ghost btn-sm" onclick="addPollOpt()" style="margin-top:0.25rem">+ Ajouter une option</button>` : ''}`;
}

function addPollOpt() { if (pollOptions.length < 4) { pollOptions.push(''); renderPollBuilder(); } }
function removePollOpt(i) { pollOptions.splice(i, 1); renderPollBuilder(); }

function submitPost() {
  const text = document.getElementById('compose-text').value.trim();
  if (!text && !pendingImage) { toast('Écris quelque chose !', 'error'); return; }
  if (text.length > 500) { toast('Trop long ! Max 500 caractères.', 'error'); return; }

  let poll = null;
  if (pendingPoll !== null) {
    const opts = pollOptions.filter(o => o.trim());
    if (opts.length < 2) { toast('Un sondage nécessite au moins 2 options.', 'error'); return; }
    poll = { options: opts.map(o => ({ text: o, votes: [] })) };
  }

  const tags = (text.match(/#([a-zA-Z0-9_\u00C0-\u017F]+)/g) || []).map(t => t.slice(1).toLowerCase());
  const posts = LS('nx_posts', []);
  const post = {
    id: Date.now().toString(), userId: currentUser.id, text, tags,
    image: pendingImage || null, poll,
    mood: pendingMood, likes: [], reposts: 0, createdAt: Date.now()
  };
  posts.unshift(post);
  LSset('nx_posts', posts);

  document.getElementById('compose-text').value = '';
  updateCharCount();
  clearImage();
  document.getElementById('poll-preview').style.display = 'none';
  pendingPoll = null; pendingMood = null; pollOptions = ['', ''];
  document.querySelectorAll('.mood-chip').forEach(c => c.classList.remove('selected'));

  renderFeed();
  renderTrends();
  notifyFollowers(post);
  toast('Post publié ! 🚀', 'success');
}

function notifyFollowers(post) {
  const users = LS('nx_users', []);
  const followers = users.filter(u => (u.following || []).includes(currentUser.id));
  const notifs = LS('nx_notifs', []);
  followers.forEach(u => notifs.unshift({
    id: Date.now().toString() + Math.random(),
    type: 'post', fromId: currentUser.id, toId: u.id, postId: post.id,
    read: false, createdAt: Date.now()
  }));
  LSset('nx_notifs', notifs);
  updateNotifBadge();
}

// ════════════════════════════════════════
// LIKES
// ════════════════════════════════════════
function toggleLike(postId) {
  const posts = LS('nx_posts', []);
  const post = posts.find(p => p.id === postId);
  if (!post) return;
  post.likes = post.likes || [];
  const idx = post.likes.indexOf(currentUser.id);
  if (idx > -1) { post.likes.splice(idx, 1); }
  else {
    post.likes.push(currentUser.id);
    if (post.userId !== currentUser.id) pushNotif('like', post.userId, postId);
  }
  LSset('nx_posts', posts);
  refreshPostCard(postId);
}

// ════════════════════════════════════════
// COMMENTS
// ════════════════════════════════════════
function toggleComments(postId) {
  const wrap = document.getElementById('post-' + postId);
  if (!wrap) return;
  const cs = wrap.querySelector('.comments-section');
  if (cs) { cs.remove(); return; }
  const div = document.createElement('div');
  div.innerHTML = renderComments(postId);
  const newCs = div.firstElementChild;
  if (newCs) wrap.appendChild(newCs);
}

function addComment(postId) {
  const inp = document.getElementById('cmt-' + postId);
  if (!inp) return;
  const text = inp.value.trim();
  if (!text) return;
  const comments = LS('nx_comments_' + postId, []);
  comments.push({ id: Date.now().toString(), userId: currentUser.id, text, likes: [], createdAt: Date.now() });
  LSset('nx_comments_' + postId, comments);
  inp.value = '';
  const posts = LS('nx_posts', []);
  const post = posts.find(p => p.id === postId);
  if (post && post.userId !== currentUser.id) pushNotif('comment', post.userId, postId);
  // refresh comment section
  const wrap = document.getElementById('post-' + postId);
  if (wrap) {
    const cs = wrap.querySelector('.comments-section');
    if (cs) { const div = document.createElement('div'); div.innerHTML = renderComments(postId); cs.replaceWith(div.firstElementChild); }
  }
  toast('Commentaire ajouté 💬', 'success');
}

function likeComment(postId, commentId) {
  const comments = LS('nx_comments_' + postId, []);
  const c = comments.find(x => x.id === commentId);
  if (!c) return;
  c.likes = c.likes || [];
  const idx = c.likes.indexOf(currentUser.id);
  if (idx > -1) c.likes.splice(idx, 1); else c.likes.push(currentUser.id);
  LSset('nx_comments_' + postId, comments);
  const wrap = document.getElementById('post-' + postId);
  if (wrap) {
    const cs = wrap.querySelector('.comments-section');
    if (cs) { const div = document.createElement('div'); div.innerHTML = renderComments(postId); cs.replaceWith(div.firstElementChild); }
  }
}

// ════════════════════════════════════════
// POLL VOTE
// ════════════════════════════════════════
function votePoll(postId, optIdx) {
  const posts = LS('nx_posts', []);
  const post = posts.find(p => p.id === postId);
  if (!post || !post.poll) return;
  const hasVoted = post.poll.options.some(o => (o.votes || []).includes(currentUser.id));
  if (hasVoted) { toast('Tu as déjà voté !', 'info'); return; }
  post.poll.options[optIdx].votes = post.poll.options[optIdx].votes || [];
  post.poll.options[optIdx].votes.push(currentUser.id);
  LSset('nx_posts', posts);
  refreshPostCard(postId);
  toast('Vote enregistré ! 📊', 'success');
}

// ════════════════════════════════════════
// BOOKMARKS
// ════════════════════════════════════════
function isBookmarked(postId) { return LS('nx_bm_' + currentUser.id, []).includes(postId); }

function toggleBookmark(postId) {
  const bms = LS('nx_bm_' + currentUser.id, []);
  const idx = bms.indexOf(postId);
  if (idx > -1) { bms.splice(idx, 1); toast('Signet supprimé', 'info'); }
  else { bms.push(postId); toast('Ajouté aux signets 🔖', 'success'); }
  LSset('nx_bm_' + currentUser.id, bms);
  refreshPostCard(postId);
}

function renderBookmarks() {
  const bms = LS('nx_bm_' + currentUser.id, []);
  const posts = LS('nx_posts', []);
  const bookmarked = bms.map(id => posts.find(p => p.id === id)).filter(Boolean);
  const el = document.getElementById('bookmark-posts');
  if (!bookmarked.length) { el.innerHTML = `<div class="empty-state"><div class="es-icon">🔖</div><h3>Aucun signet</h3><p>Sauvegarde des posts pour les retrouver ici.</p></div>`; return; }
  el.innerHTML = bookmarked.map(p => renderPostCard(p)).join('');
}

function clearBookmarks() {
  if (!confirm('Effacer tous les signets ?')) return;
  LSset('nx_bm_' + currentUser.id, []);
  renderBookmarks();
  toast('Signets effacés', 'info');
}

// ════════════════════════════════════════
// POST MENU
// ════════════════════════════════════════
function toggleMenu(postId, e) {
  e.stopPropagation();
  if (openMenuId && openMenuId !== postId) {
    const prev = document.getElementById('menu-' + openMenuId);
    if (prev) prev.style.display = 'none';
  }
  const m = document.getElementById('menu-' + postId);
  if (m) m.style.display = m.style.display === 'none' ? 'block' : 'none';
  openMenuId = m && m.style.display === 'block' ? postId : null;
}
document.addEventListener('click', () => {
  if (openMenuId) { const m = document.getElementById('menu-' + openMenuId); if (m) m.style.display = 'none'; openMenuId = null; }
});

function deletePost(postId) {
  if (!confirm('Supprimer ce post ?')) return;
  let posts = LS('nx_posts', []);
  posts = posts.filter(p => p.id !== postId);
  LSset('nx_posts', posts);
  const wrap = document.querySelector('#post-' + postId)?.closest('.post-wrap');
  if (wrap) wrap.remove();
  renderTrends();
  toast('Post supprimé', 'info');
}

function pinPost(postId) {
  const users = LS('nx_users', []);
  const me = users.find(u => u.id === currentUser.id);
  me.pinnedPost = me.pinnedPost === postId ? null : postId;
  LSset('nx_users', users);
  currentUser = me;
  toast(me.pinnedPost ? 'Post épinglé 📌' : 'Post désépinglé', 'info');
  if (currentProfileId === currentUser.id) renderProfile(currentUser.id);
}

function reportPost() { toast('Post signalé. Merci ! 🚩', 'info'); }

function sharePost(postId) {
  if (navigator.clipboard) navigator.clipboard.writeText(location.href + '#post-' + postId);
  toast('Lien copié ! 🔗', 'success');
}

function repost(postId) {
  const posts = LS('nx_posts', []);
  const orig = posts.find(p => p.id === postId);
  if (!orig) return;
  orig.reposts = (orig.reposts || 0) + 1;
  const newPost = { ...orig, id: Date.now().toString(), userId: currentUser.id, text: '🔁 ' + orig.text, createdAt: Date.now(), likes: [], reposts: 0, poll: null };
  posts.unshift(newPost);
  LSset('nx_posts', posts);
  renderFeed();
  toast('Reposté ! 🔁', 'success');
}

function refreshPostCard(postId) {
  const posts = LS('nx_posts', []);
  const post = posts.find(p => p.id === postId);
  const wrap = document.querySelector('#post-' + postId)?.closest('.post-wrap');
  if (!wrap) return;
  const hadComments = !!wrap.querySelector('.comments-section');
  const tmp = document.createElement('div');
  tmp.innerHTML = renderPostCard(post, { showComments: hadComments });
  wrap.replaceWith(tmp.firstElementChild);
}

// ════════════════════════════════════════
// PROFILE
// ════════════════════════════════════════
function drawProfileCover(color1, color2) {
  const canvas = document.getElementById('profile-cover');
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  canvas.width = canvas.offsetWidth || 800;
  canvas.height = 200;
  const grad = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
  grad.addColorStop(0, color1 || '#2d1f5e');
  grad.addColorStop(1, color2 || '#1f5e5e');
  ctx.fillStyle = grad;
  ctx.fillRect(0, 0, canvas.width, canvas.height);
  // dots pattern
  ctx.fillStyle = 'rgba(255,255,255,0.04)';
  for (let x = 0; x < canvas.width; x += 30) {
    for (let y = 0; y < canvas.height; y += 30) {
      ctx.beginPath(); ctx.arc(x, y, 1.5, 0, Math.PI * 2); ctx.fill();
    }
  }
}

function switchProfileTab(tab, btn) {
  profileTab = tab;
  document.querySelectorAll('.profile-tab').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderProfilePosts(currentProfileId);
}

function renderProfile(uid) {
  const users = LS('nx_users', []);
  const user = users.find(u => u.id === uid);
  if (!user) return;
  refreshCurrentUser();
  const avEl = document.getElementById('profile-av');
  avEl.textContent = user.avatar;
  avEl.style.background = user.avatarColor;
  document.getElementById('profile-name').textContent = user.name;
  document.getElementById('profile-handle').textContent = '@' + user.handle;
  document.getElementById('profile-bio').textContent = user.bio || '';

  const metaEl = document.getElementById('profile-meta');
  let meta = [];
  if (user.location) meta.push(`📍 ${esc(user.location)}`);
  if (user.website) meta.push(`🔗 <a href="${esc(user.website)}" target="_blank" style="color:var(--accent2)">${esc(user.website.replace(/https?:\/\//,''))}</a>`);
  meta.push(`📅 Membre depuis ${new Date(user.createdAt).toLocaleDateString('fr-FR',{month:'long',year:'numeric'})}`);
  metaEl.innerHTML = meta.map(m => `<span>${m}</span>`).join('');

  const posts = LS('nx_posts', []).filter(p => p.userId === uid);
  document.getElementById('p-posts').textContent = posts.length;
  document.getElementById('p-followers').textContent = (user.followers || []).length;
  document.getElementById('p-following').textContent = (user.following || []).length;

  const actEl = document.getElementById('profile-actions');
  if (uid === currentUser.id) {
    actEl.innerHTML = `<button class="btn btn-ghost" onclick="openEditProfile()">✏️ Modifier</button>`;
  } else {
    const isFollowing = (currentUser.following || []).includes(uid);
    const isMutual = (user.following || []).includes(currentUser.id);
    actEl.innerHTML = `
      <button class="btn ${isFollowing ? 'btn-ghost' : 'btn-primary'}" onclick="toggleFollow('${uid}')">${isFollowing ? 'Se désabonner' : (isMutual ? '↩ Suivre en retour' : 'Suivre')}</button>
      <button class="btn btn-ghost" onclick="startMsgWithUser('${uid}')">✉️ Message</button>`;
  }

  drawProfileCover(user.avatarColor, shiftColor(user.avatarColor));
  document.querySelectorAll('.profile-tab').forEach(b => b.classList.remove('active'));
  document.querySelector('.profile-tab').classList.add('active');
  profileTab = 'posts';
  renderProfilePosts(uid);
}

function renderProfilePosts(uid) {
  const allPosts = LS('nx_posts', []);
  let posts;
  if (profileTab === 'posts') {
    posts = allPosts.filter(p => p.userId === uid).sort((a, b) => b.createdAt - a.createdAt);
  } else if (profileTab === 'replies') {
    // posts they commented on
    const commentedIds = allPosts.map(p => {
      const comments = LS('nx_comments_' + p.id, []);
      return comments.some(c => c.userId === uid) ? p.id : null;
    }).filter(Boolean);
    posts = allPosts.filter(p => commentedIds.includes(p.id)).sort((a, b) => b.createdAt - a.createdAt);
  } else if (profileTab === 'media') {
    posts = allPosts.filter(p => p.userId === uid && p.image).sort((a, b) => b.createdAt - a.createdAt);
  } else if (profileTab === 'likes') {
    posts = allPosts.filter(p => (p.likes || []).includes(uid)).sort((a, b) => b.createdAt - a.createdAt);
  }
  const el = document.getElementById('profile-posts');
  if (!posts.length) { el.innerHTML = `<div class="empty-state"><div class="es-icon">📝</div><h3>Aucun contenu</h3><p>Rien ici pour l'instant.</p></div>`; return; }
  el.innerHTML = posts.map(p => renderPostCard(p)).join('');
}

function shiftColor(hex) {
  // complementary-ish shift
  const num = parseInt(hex.slice(1), 16);
  return '#' + ((num + 0x1e1e5e) & 0xffffff).toString(16).padStart(6, '0');
}

function toggleFollow(uid) {
  const users = LS('nx_users', []);
  const me = users.find(u => u.id === currentUser.id);
  const them = users.find(u => u.id === uid);
  if (!me || !them) return;
  me.following = me.following || [];
  them.followers = them.followers || [];
  const idx = me.following.indexOf(uid);
  if (idx > -1) {
    me.following.splice(idx, 1);
    const fi = them.followers.indexOf(currentUser.id);
    if (fi > -1) them.followers.splice(fi, 1);
    toast(`Désabonné de @${them.handle}`, 'info');
  } else {
    me.following.push(uid);
    them.followers.push(currentUser.id);
    pushNotif('follow', uid, null);
    toast(`Tu suis maintenant @${them.handle} 🎉`, 'success');
  }
  LSset('nx_users', users);
  currentUser = me;
  renderProfile(uid);
  renderSuggestions();
}

function showFollowModal(type) {
  const users = LS('nx_users', []);
  const profUser = users.find(u => u.id === currentProfileId);
  if (!profUser) return;
  let list = [];
  let title = '';
  if (type === 'followers') {
    title = `Abonnés (${(profUser.followers||[]).length})`;
    list = (profUser.followers || []).map(id => users.find(u => u.id === id)).filter(Boolean);
  } else if (type === 'following') {
    title = `Abonnements (${(profUser.following||[]).length})`;
    list = (profUser.following || []).map(id => users.find(u => u.id === id)).filter(Boolean);
  } else return;
  document.getElementById('follow-modal-title').innerHTML = title + ` <button class="modal-close" onclick="closeModal('modal-follows')">✕</button>`;
  const el = document.getElementById('follow-list');
  if (!list.length) { el.innerHTML = `<p style="color:var(--muted);padding:1rem 0">Aucun utilisateur.</p>`; }
  else el.innerHTML = list.map(u => `<div class="follow-list-item">
    <div class="avatar sz-md" style="background:${esc(u.avatarColor)};cursor:pointer" onclick="closeModal('modal-follows');gotoProfile('${esc(u.id)}')">${u.avatar}</div>
    <div style="flex:1;cursor:pointer" onclick="closeModal('modal-follows');gotoProfile('${esc(u.id)}')">
      <div style="font-weight:600;font-size:0.9rem">${esc(u.name)}</div>
      <div style="font-size:0.8rem;color:var(--muted)">@${esc(u.handle)}</div>
    </div>
    ${u.id !== currentUser.id ? `<button class="btn btn-ghost btn-sm" onclick="toggleFollow('${esc(u.id)}')">${(currentUser.following||[]).includes(u.id)?'Désabonner':'Suivre'}</button>` : ''}
  </div>`).join('');
  document.getElementById('modal-follows').classList.add('open');
}

// ════════════════════════════════════════
// NOTIFICATIONS
// ════════════════════════════════════════
function pushNotif(type, toId, postId) {
  if (!toId || toId === currentUser.id) return;
  const notifs = LS('nx_notifs', []);
  notifs.unshift({ id: Date.now().toString() + Math.random(), type, fromId: currentUser.id, toId, postId, read: false, createdAt: Date.now() });
  LSset('nx_notifs', notifs);
  updateNotifBadge();
}

function renderNotifications() {
  const notifs = LS('nx_notifs', []).filter(n => n.toId === currentUser.id).slice(0, 50);
  const users = LS('nx_users', []);
  const posts = LS('nx_posts', []);
  const el = document.getElementById('notif-list');
  if (!notifs.length) { el.innerHTML = `<div class="empty-state"><div class="es-icon">🔔</div><h3>Aucune notification</h3><p>Les interactions apparaîtront ici.</p></div>`; return; }
  el.innerHTML = notifs.map(n => {
    const from = users.find(u => u.id === n.fromId) || { name: 'Quelqu\'un', avatar: '❓', avatarColor: '#333', id: '' };
    const post = n.postId ? posts.find(p => p.id === n.postId) : null;
    const iconMap = { like: '❤️', comment: '💬', follow: '👤', post: '📝' };
    const textMap = {
      like: `<strong>${esc(from.name)}</strong> a aimé ton post`,
      comment: `<strong>${esc(from.name)}</strong> a commenté ton post`,
      follow: `<strong>${esc(from.name)}</strong> a commencé à te suivre`,
      post: `<strong>${esc(from.name)}</strong> a publié un nouveau post`
    };
    const preview = post ? `<div class="notif-preview">${esc(post.text.substring(0,80))}${post.text.length>80?'…':''}</div>` : '';
    return `<div class="notif-item ${n.read ? '' : 'unread'}" onclick="n.postId&&gotoProfile('${esc(from.id)}')">
      <div class="notif-icon" style="background:var(--bg3)">${iconMap[n.type]||'🔔'}</div>
      <div class="notif-body">
        <div class="notif-text">${textMap[n.type]||'Nouvelle notification'}</div>
        ${preview}
        <div class="notif-time">${timeAgo(n.createdAt)}</div>
      </div>
      ${n.read ? '' : '<div class="notif-dot"></div>'}
    </div>`;
  }).join('');
}

function markAllRead() {
  const notifs = LS('nx_notifs', []);
  notifs.forEach(n => { if (n.toId === currentUser.id) n.read = true; });
  LSset('nx_notifs', notifs);
  updateNotifBadge();
  renderNotifications();
}

function updateNotifBadge() {
  const count = LS('nx_notifs', []).filter(n => n.toId === currentUser.id && !n.read).length;
  const b = document.getElementById('notif-badge');
  if (b) { b.style.display = count > 0 ? '' : 'none'; b.textContent = count > 9 ? '9+' : count; }
}

// ════════════════════════════════════════
// MESSAGES
// ════════════════════════════════════════
function getConvId(uid1, uid2) {
  return [uid1, uid2].sort().join('_');
}

function renderConvList(filter = '') {
  const users = LS('nx_users', []);
  const convs = LS('nx_convs_' + currentUser.id, []);
  const filtered = filter ? convs.filter(c => {
    const u = users.find(x => x.id === c.otherId);
    return u && (u.name.toLowerCase().includes(filter.toLowerCase()) || u.handle.toLowerCase().includes(filter.toLowerCase()));
  }) : convs;
  const el = document.getElementById('conv-list');
  if (!filtered.length) { el.innerHTML = `<div style="padding:2rem;text-align:center;color:var(--muted);font-size:0.875rem">Aucune conversation</div>`; return; }
  el.innerHTML = filtered.map(c => {
    const u = users.find(x => x.id === c.otherId) || { name: '?', avatar: '❓', avatarColor: '#333', handle: '?' };
    const msgs = LS('nx_msgs_' + c.convId, []);
    const last = msgs[msgs.length - 1];
    const unread = msgs.filter(m => m.senderId !== currentUser.id && !m.read).length;
    return `<div class="conv-item ${activeConvId === c.convId ? 'active' : ''}" onclick="openConv('${esc(c.convId)}','${esc(c.otherId)}')">
      <div class="avatar sz-sm" style="background:${esc(u.avatarColor)}">${u.avatar}</div>
      <div class="conv-info">
        <div class="conv-name">${esc(u.name)}</div>
        <div class="conv-preview">${last ? esc(last.text.substring(0,35)) + (last.text.length>35?'…':'') : 'Nouvelle conversation'}</div>
      </div>
      <div style="display:flex;flex-direction:column;align-items:flex-end;gap:0.25rem">
        ${last ? `<span class="conv-time">${timeAgo(last.createdAt)}</span>` : ''}
        ${unread > 0 ? `<div class="conv-unread"></div>` : ''}
      </div>
    </div>`;
  }).join('');
}

function filterConvs(val) { renderConvList(val); }

function openConv(convId, otherId) {
  activeConvId = convId;
  const users = LS('nx_users', []);
  const other = users.find(u => u.id === otherId);
  if (!other) return;
  // mark read
  const msgs = LS('nx_msgs_' + convId, []);
  msgs.forEach(m => { if (m.senderId !== currentUser.id) m.read = true; });
  LSset('nx_msgs_' + convId, msgs);
  renderConvList();
  const main = document.getElementById('msg-main');
  main.innerHTML = `
    <div class="msg-header">
      <div class="avatar sz-sm" style="background:${esc(other.avatarColor)};cursor:pointer" onclick="gotoProfile('${esc(other.id)}')">${other.avatar}</div>
      <div style="flex:1">
        <div style="font-weight:600;font-size:0.9rem;cursor:pointer" onclick="gotoProfile('${esc(other.id)}')">${esc(other.name)}</div>
        <div style="font-size:0.75rem;color:var(--muted)">@${esc(other.handle)}</div>
      </div>
    </div>
    <div class="msg-body" id="msg-body-${convId}"></div>
    <div class="msg-footer">
      <input type="text" id="msg-input-${convId}" placeholder="Écris un message…" onkeydown="if(event.key==='Enter')sendMsg('${esc(convId)}','${esc(otherId)}')">
      <button class="btn btn-primary btn-sm" onclick="sendMsg('${esc(convId)}','${esc(otherId)}')">Envoyer</button>
    </div>`;
  renderMsgBody(convId);
}

function renderMsgBody(convId) {
  const msgs = LS('nx_msgs_' + convId, []);
  const el = document.getElementById('msg-body-' + convId);
  if (!el) return;
  if (!msgs.length) { el.innerHTML = `<div class="msg-empty"><span>Commencer la conversation…</span></div>`; return; }
  el.innerHTML = msgs.map(m => {
    const mine = m.senderId === currentUser.id;
    return `<div class="msg-bubble-wrap ${mine ? 'mine' : ''}">
      <div class="msg-bubble ${mine ? 'mine' : 'them'}">
        ${esc(m.text)}
        <div class="msg-bubble-time">${timeAgo(m.createdAt)}</div>
      </div>
    </div>`;
  }).join('');
  el.scrollTop = el.scrollHeight;
}

function sendMsg(convId, otherId) {
  const inp = document.getElementById('msg-input-' + convId);
  if (!inp) return;
  const text = inp.value.trim();
  if (!text) return;
  const msgs = LS('nx_msgs_' + convId, []);
  msgs.push({ id: Date.now().toString(), senderId: currentUser.id, text, read: false, createdAt: Date.now() });
  LSset('nx_msgs_' + convId, msgs);
  inp.value = '';
  // ensure conv in both users' lists
  addConvRecord(currentUser.id, otherId, convId);
  addConvRecord(otherId, currentUser.id, convId);
  renderMsgBody(convId);
  renderConvList();
}

function addConvRecord(userId, otherId, convId) {
  const convs = LS('nx_convs_' + userId, []);
  if (!convs.find(c => c.convId === convId)) {
    convs.push({ convId, otherId });
    LSset('nx_convs_' + userId, convs);
  }
}

function openNewMsg() {
  document.getElementById('newmsg-search').value = '';
  document.getElementById('newmsg-results').innerHTML = '';
  document.getElementById('modal-newmsg').classList.add('open');
}

function searchForMsg() {
  const q = document.getElementById('newmsg-search').value.trim().toLowerCase();
  const users = LS('nx_users', []).filter(u => u.id !== currentUser.id);
  const results = q ? users.filter(u => u.name.toLowerCase().includes(q) || u.handle.includes(q)) : users.slice(0, 5);
  const el = document.getElementById('newmsg-results');
  el.innerHTML = results.map(u => `<div class="follow-list-item" style="cursor:pointer" onclick="startMsgWithUser('${esc(u.id)}')">
    <div class="avatar sz-sm" style="background:${esc(u.avatarColor)}">${u.avatar}</div>
    <div><div style="font-weight:600;font-size:0.9rem">${esc(u.name)}</div><div style="font-size:0.78rem;color:var(--muted)">@${esc(u.handle)}</div></div>
  </div>`).join('');
}

function startMsgWithUser(uid) {
  closeModal('modal-newmsg');
  const convId = getConvId(currentUser.id, uid);
  addConvRecord(currentUser.id, uid, convId);
  addConvRecord(uid, currentUser.id, convId);
  gotoPage('messages', document.querySelectorAll('.nav-item')[2]);
  setTimeout(() => openConv(convId, uid), 50);
}

// ════════════════════════════════════════
// EXPLORE / SEARCH
// ════════════════════════════════════════
let searchFilterVal = 'all';

function setSearchFilter(f, btn) {
  searchFilterVal = f;
  document.querySelectorAll('.filter-chip').forEach(c => c.classList.remove('active'));
  btn.classList.add('active');
  doSearch();
}

function renderExploreTrends() {
  const posts = LS('nx_posts', []);
  const tagMap = {};
  posts.forEach(p => (p.tags || []).forEach(t => { tagMap[t] = (tagMap[t] || 0) + 1; }));
  const sorted = Object.entries(tagMap).sort((a, b) => b[1] - a[1]).slice(0, 10);
  const el = document.getElementById('explore-trends');
  if (!sorted.length) { el.innerHTML = `<div class="empty-state"><div class="es-icon">🔍</div><h3>Aucune tendance</h3><p>Publie des posts avec des hashtags !</p></div>`; return; }
  el.innerHTML = sorted.map(([tag, count], i) => `<div class="trend-item" style="padding:0.9rem 1.5rem;border-bottom:1px solid var(--border)" onclick="searchByTag('${esc(tag)}')">
    <div>
      <div style="font-size:0.72rem;color:var(--muted);margin-bottom:0.1rem">Tendance #${i+1}</div>
      <div class="trend-tag">#${esc(tag)}</div>
    </div>
    <div class="trend-badge">${count} post${count>1?'s':''}</div>
  </div>`).join('');
}

function doSearch() {
  const q = document.getElementById('search-q').value.trim().toLowerCase();
  const el = document.getElementById('search-results');
  if (!q) { el.innerHTML = `<div style="padding:1.5rem 1.5rem 0.5rem;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--muted);font-weight:600">Tendances du moment</div><div id="explore-trends"></div>`; renderExploreTrends(); return; }
  const users = LS('nx_users', []);
  const posts = LS('nx_posts', []);
  const matchUsers = users.filter(u => u.name.toLowerCase().includes(q) || u.handle.includes(q));
  const matchPosts = posts.filter(p => p.text.toLowerCase().includes(q) || (p.tags || []).some(t => t.includes(q.replace('#', ''))));
  const matchTags = [...new Set(posts.flatMap(p => p.tags || []).filter(t => t.includes(q.replace('#', ''))))];
  let html = '';
  const showUsers = searchFilterVal === 'all' || searchFilterVal === 'users';
  const showPosts = searchFilterVal === 'all' || searchFilterVal === 'posts';
  const showTags = searchFilterVal === 'all' || searchFilterVal === 'tags';
  if (showUsers && matchUsers.length) {
    html += `<div style="padding:0.75rem 1.5rem;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--muted);font-weight:600">Personnes</div>`;
    html += matchUsers.map(u => {
      const mutual = (u.following || []).includes(currentUser.id) && (currentUser.following || []).includes(u.id);
      return `<div style="display:flex;align-items:center;gap:0.75rem;padding:0.875rem 1.5rem;border-bottom:1px solid var(--border);cursor:pointer" onclick="gotoProfile('${esc(u.id)}')">
        <div class="avatar sz-md" style="background:${esc(u.avatarColor)}">${u.avatar}</div>
        <div style="flex:1">
          <div style="font-weight:600;font-size:0.9rem">${esc(u.name)}</div>
          <div style="font-size:0.8rem;color:var(--muted)">@${esc(u.handle)}</div>
          ${mutual ? `<div style="font-size:0.72rem;color:var(--teal)">Abonnements mutuels</div>` : ''}
        </div>
        ${u.id !== currentUser.id ? `<button class="btn btn-ghost btn-sm" onclick="event.stopPropagation();toggleFollow('${esc(u.id)}')">${(currentUser.following||[]).includes(u.id)?'Désabonner':'Suivre'}</button>` : ''}
      </div>`;
    }).join('');
  }
  if (showTags && matchTags.length) {
    html += `<div style="padding:0.75rem 1.5rem;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--muted);font-weight:600">Hashtags</div>`;
    html += matchTags.map(t => `<div style="padding:0.75rem 1.5rem;border-bottom:1px solid var(--border);cursor:pointer" onclick="searchByTag('${esc(t)}')">
      <span class="post-tag" style="font-size:0.9rem">#${esc(t)}</span>
    </div>`).join('');
  }
  if (showPosts && matchPosts.length) {
    html += `<div style="padding:0.75rem 1.5rem;font-size:0.78rem;text-transform:uppercase;letter-spacing:0.08em;color:var(--muted);font-weight:600">Posts</div>`;
    html += matchPosts.slice(0, 15).map(p => renderPostCard(p)).join('');
  }
  if (!matchUsers.length && !matchPosts.length && !matchTags.length) {
    html = `<div class="empty-state"><div class="es-icon">🔍</div><h3>Aucun résultat</h3><p>Essaie un autre terme.</p></div>`;
  }
  el.innerHTML = html;
}

function searchByTag(tag) {
  gotoPage('explore', document.querySelectorAll('.nav-item')[1]);
  const inp = document.getElementById('search-q');
  inp.value = '#' + tag;
  searchFilterVal = 'posts';
  document.querySelectorAll('.filter-chip').forEach((c, i) => c.classList.toggle('active', i === 2));
  doSearch();
}

// ════════════════════════════════════════
// TRENDS & SUGGESTIONS
// ════════════════════════════════════════
function renderTrends() {
  const posts = LS('nx_posts', []);
  const tagMap = {};
  posts.forEach(p => (p.tags || []).forEach(t => { tagMap[t] = (tagMap[t] || 0) + 1; }));
  const sorted = Object.entries(tagMap).sort((a, b) => b[1] - a[1]).slice(0, 5);
  const el = document.getElementById('trends-list');
  if (!sorted.length) { el.innerHTML = `<p style="color:var(--muted);font-size:0.875rem">Aucune tendance pour l'instant.</p>`; return; }
  el.innerHTML = sorted.map(([tag, count]) => `<div class="trend-item" onclick="searchByTag('${esc(tag)}')">
    <div><div class="trend-tag">#${esc(tag)}</div><div class="trend-meta">${count} post${count>1?'s':''}</div></div>
    <span class="trend-badge">🔥</span>
  </div>`).join('');
}

function renderSuggestions(refresh = false) {
  refreshCurrentUser();
  const users = LS('nx_users', []);
  let notFollowing = users.filter(u => u.id !== currentUser.id && !(currentUser.following || []).includes(u.id));
  if (refresh) notFollowing = notFollowing.sort(() => Math.random() - 0.5);
  notFollowing = notFollowing.slice(0, 4);
  const el = document.getElementById('suggest-list');
  if (!notFollowing.length) { el.innerHTML = `<p style="color:var(--muted);font-size:0.875rem">Tu suis tout le monde ! 🎉</p>`; return; }
  el.innerHTML = notFollowing.map(u => {
    const mutual = (u.following || []).includes(currentUser.id);
    return `<div class="suggest-item">
      <div class="avatar sz-sm" style="background:${esc(u.avatarColor)};cursor:pointer" onclick="gotoProfile('${esc(u.id)}')">${u.avatar}</div>
      <div class="suggest-info" style="cursor:pointer" onclick="gotoProfile('${esc(u.id)}')">
        <div class="suggest-name">${esc(u.name)}</div>
        <div class="suggest-handle">@${esc(u.handle)}</div>
        ${mutual ? `<div class="suggest-mutual">Te suit déjà</div>` : ''}
      </div>
      <button class="btn btn-ghost btn-sm" onclick="toggleFollow('${esc(u.id)}')">Suivre</button>
    </div>`;
  }).join('');
}

// ════════════════════════════════════════
// EDIT PROFILE
// ════════════════════════════════════════
function openEditProfile() {
  refreshCurrentUser();
  document.getElementById('ep-name').value = currentUser.name;
  document.getElementById('ep-handle').value = currentUser.handle;
  document.getElementById('ep-bio').value = currentUser.bio || '';
  document.getElementById('ep-website').value = currentUser.website || '';
  document.getElementById('ep-location').value = currentUser.location || '';
  buildAvatarPick('ep-avatar-pick', 'pickAvatarEdit');
  const curIdx = AV_EMOJIS.indexOf(currentUser.avatar);
  document.querySelectorAll('#ep-avatar-pick .av-opt').forEach((el, i) => el.classList.toggle('selected', i === curIdx));
  selectedAvatarEdit = { emoji: currentUser.avatar, color: currentUser.avatarColor };
  document.getElementById('modal-editprofile').classList.add('open');
}

function saveProfile() {
  const name = document.getElementById('ep-name').value.trim();
  const handle = document.getElementById('ep-handle').value.trim().replace('@', '').toLowerCase().replace(/\s/g, '');
  const bio = document.getElementById('ep-bio').value.trim();
  const website = document.getElementById('ep-website').value.trim();
  const location = document.getElementById('ep-location').value.trim();
  if (!name) { toast('Le nom ne peut pas être vide.', 'error'); return; }
  if (!handle) { toast('Nom d\'utilisateur requis.', 'error'); return; }
  const users = LS('nx_users', []);
  const conflict = users.find(u => u.handle === handle && u.id !== currentUser.id);
  if (conflict) { toast('Nom d\'utilisateur déjà pris.', 'error'); return; }
  const me = users.find(u => u.id === currentUser.id);
  if (!me) return;
  me.name = name; me.handle = handle; me.bio = bio; me.website = website; me.location = location;
  if (selectedAvatarEdit) { me.avatar = selectedAvatarEdit.emoji; me.avatarColor = selectedAvatarEdit.color; }
  LSset('nx_users', users);
  currentUser = me;
  updateSidebar();
  closeModal('modal-editprofile');
  toast('Profil mis à jour ! ✨', 'success');
  if (currentProfileId === currentUser.id) renderProfile(currentUser.id);
}

function closeModal(id) { document.getElementById(id).classList.remove('open'); }
document.querySelectorAll('.modal-overlay').forEach(m => m.addEventListener('click', e => { if (e.target === m) m.classList.remove('open'); }));

// ════════════════════════════════════════
// TOAST
// ════════════════════════════════════════
function toast(msg, type = 'info') {
  const icons = { success: '✅', error: '❌', info: 'ℹ️' };
  const t = document.createElement('div');
  t.className = `toast ${type}`;
  t.innerHTML = `<span class="toast-icon">${icons[type]}</span><span>${msg}</span>`;
  document.getElementById('toast-wrap').appendChild(t);
  setTimeout(() => { t.classList.add('fadeOut'); setTimeout(() => t.remove(), 300); }, 3200);
}

// ════════════════════════════════════════
// UTILS
// ════════════════════════════════════════
function esc(s) {
  if (s == null) return '';
  return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');
}

function timeAgo(ts) {
  const d = Date.now() - ts, s = Math.floor(d / 1000), m = Math.floor(s / 60), h = Math.floor(m / 60), day = Math.floor(h / 24);
  if (s < 60) return 'À l\'instant';
  if (m < 60) return `il y a ${m} min`;
  if (h < 24) return `il y a ${h}h`;
  if (day < 7) return `il y a ${day}j`;
  return new Date(ts).toLocaleDateString('fr-FR', { day: 'numeric', month: 'short' });
}

// ════════════════════════════════════════
// BOOT
// ════════════════════════════════════════
(function init() {
  buildAvatarPick('avatar-pick', 'pickAvatar');
  // Select first avatar by default
  const firstAv = document.querySelector('#avatar-pick .av-opt');
  if (firstAv) { firstAv.classList.add('selected'); selectedAvatar = { emoji: AV_EMOJIS[0], color: AV_COLORS[0] }; }

  const sessionId = LS('nx_session', null);
  if (sessionId) {
    const users = LS('nx_users', []);
    const user = users.find(u => u.id === sessionId);
    if (user) { currentUser = user; launchApp(); return; }
  }
  document.getElementById('auth-screen').style.display = 'flex';
})();
</script>
</body>
</html>
