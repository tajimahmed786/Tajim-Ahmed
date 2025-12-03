<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Tajim Ahmed — Animated GitHub Profile</title>
  <style>
    :root{
      --bg1:#0f172a; /* deep navy */
      --bg2:#051025; /* darker */
      --accent1:#7c3aed; /* violet */
      --accent2:#06b6d4; /* teal */
      --glass: rgba(255,255,255,0.06);
      --glass-2: rgba(255,255,255,0.03);
      --card-shadow: 0 8px 30px rgba(2,6,23,0.6);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial;
    }
    html,body{height:100%;margin:0;background:radial-gradient(circle at 10% 20%, rgba(124,58,237,0.12), transparent 5%), radial-gradient(circle at 90% 80%, rgba(6,182,212,0.06), transparent 12%), linear-gradient(180deg,var(--bg1),var(--bg2)); color: #e6eef8}
    .wrap{min-height:100vh;display:flex;align-items:center;justify-content:center;padding:40px}

    /* animated blob background */
    .blob-wrap{position:absolute;inset:0;overflow:hidden;pointer-events:none}
    .blob{
      position:absolute;filter:blur(60px);opacity:0.45;mix-blend-mode:screen;background:linear-gradient(45deg,var(--accent1),var(--accent2));width:600px;height:600px;border-radius:48% 52% 44% 56%/52% 46% 54% 48%;animation:blobmove 12s infinite ease-in-out;
    }
    .blob.b2{width:500px;height:500px;left:60%;top:10%;animation-duration:16s;opacity:0.28}
    .blob.b1{left:-8%;top:5%}
    @keyframes blobmove{0%{transform:translate(0,0) scale(1)}33%{transform:translate(8vw,-6vh) scale(1.08)}66%{transform:translate(-6vw,6vh) scale(0.94)}100%{transform:translate(0,0) scale(1)}}

    .card{
      position:relative;z-index:2;display:grid;grid-template-columns:260px 1fr;gap:28px;padding:28px;border-radius:18px;background:linear-gradient(135deg,var(--glass),var(--glass-2));box-shadow:var(--card-shadow);backdrop-filter: blur(8px);width:980px;max-width:95%;align-items:center;
    }

    /* left column */
    .left{display:flex;flex-direction:column;gap:18px;align-items:center}
    .avatar{width:200px;height:200px;border-radius:18px;overflow:hidden;box-shadow:0 10px 30px rgba(2,6,23,0.5);border:1px solid rgba(255,255,255,0.06);display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent)}
    .avatar img{width:100%;height:100%;object-fit:cover}
    .name{font-size:22px;font-weight:700;letter-spacing:0.2px;text-align:center}
    .role{font-size:13px;opacity:0.85;text-align:center}
    .stat-grid{display:flex;gap:10px;margin-top:6px}
    .stat{padding:10px 14px;border-radius:12px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);text-align:center}
    .stat strong{display:block;font-size:18px}
    .buttons{display:flex;gap:10px;margin-top:8px}
    .btn{padding:10px 12px;border-radius:10px;border:none;background:rgba(255,255,255,0.03);cursor:pointer;color:inherit;font-weight:600}

    /* right column */
    .right{display:flex;flex-direction:column;gap:14px}
    .headline{display:flex;align-items:center;justify-content:space-between;gap:12px}
    .title{font-size:18px;font-weight:700}
    .typewriter{font-family:monospace;font-weight:600;background:linear-gradient(90deg,var(--accent1),var(--accent2));-webkit-background-clip:text;background-clip:text;color:transparent}

    .bio{font-size:14px;line-height:1.5;opacity:0.95}

    .repo-list{display:grid;grid-template-columns:repeat(2,1fr);gap:12px;margin-top:6px}
    .repo{padding:12px;border-radius:12px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);border:1px solid rgba(255,255,255,0.03);display:flex;flex-direction:column;gap:8px}
    .repo h4{margin:0;font-size:15px}
    .repo p{margin:0;font-size:12px;opacity:0.85}
    .tag-row{display:flex;gap:8px;flex-wrap:wrap}
    .tag{font-size:12px;padding:6px 8px;border-radius:999px;background:rgba(255,255,255,0.02)}

    /* small input area */
    .controls{display:flex;gap:10px;align-items:center}
    .controls input{background:transparent;border:1px solid rgba(255,255,255,0.06);padding:8px 10px;border-radius:10px;color:inherit}

    /* subtle hover */
    .repo:hover{transform:translateY(-6px);transition:transform .22s cubic-bezier(.2,.9,.3,1)}

    /* responsive */
    @media (max-width:820px){.card{grid-template-columns:1fr;align-items:start}.avatar{width:160px;height:160px}.repo-list{grid-template-columns:1fr}}

    /* typing cursor animation */
    .cursor{display:inline-block;width:10px;height:18px;background:var(--accent2);margin-left:6px;border-radius:2px;animation:blink 1s steps(2, start) infinite}
    @keyframes blink{50%{opacity:0}}

    /* small floating animated icon */
    .floating{position:absolute;right:18px;top:18px;padding:10px;border-radius:10px;background:linear-gradient(180deg,rgba(255,255,255,0.02),transparent);backdrop-filter: blur(6px);}

  </style>
</head>
<body>
  <div class="blob-wrap" aria-hidden>
    <div class="blob b1"></div>
    <div class="blob b2"></div>
  </div>
  <div class="wrap">
    <div class="card" role="main">

      <div class="left">
        <div class="avatar" id="avatar">
          <!-- fallback avatar (generated initials) -->
          <svg width="200" height="200" viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg" aria-hidden>
            <defs><linearGradient id="g" x1="0" x2="1"><stop offset="0" stop-color="#7c3aed"/><stop offset="1" stop-color="#06b6d4"/></linearGradient></defs>
            <rect width="200" height="200" rx="18" fill="url(#g)"/>
            <text x="50%" y="54%" dominant-baseline="middle" text-anchor="middle" font-size="48" font-family="sans-serif" fill="white">TA</text>
          </svg>
        </div>
        <div class="name" id="displayName">Tajim Ahmed</div>
        <div class="role" id="displayRole">Developer • Open Source Enthusiast</div>

        <div class="stat-grid">
          <div class="stat"><strong id="followers">—</strong><span style="font-size:12px;opacity:0.85">Followers</span></div>
          <div class="stat"><strong id="repos">—</strong><span style="font-size:12px;opacity:0.85">Repos</span></div>
        </div>

        <div class="buttons">
          <button class="btn" id="copyMd">Copy README snippet</button>
          <button class="btn" id="themeToggle">✨ Theme</button>
        </div>

        <div style="font-size:12px;opacity:0.85;text-align:center;margin-top:6px">Tip: enter your GitHub username to load live data</div>
      </div>

      <div class="right">
        <div class="headline">
          <div>
            <div class="title">Animated GitHub Profile</div>
            <div class="typewriter" id="typing">Hello, I'm <span id="typedName">Tajim Ahmed</span><span class="cursor" aria-hidden></span></div>
          </div>
          <div class="floating" title="Profile controls">
            <div class="controls">
              <input placeholder="GitHub username (optional)" id="ghUsername">
              <button class="btn" id="loadBtn">Load</button>
            </div>
          </div>
        </div>

        <div class="bio" id="bio">Full-stack developer, tinkerer, and builder. I love clean code, thoughtful UX and contributing to open-source. This animated profile is a minimal, self-hosted hero section you can reuse in your GitHub README or personal site.</div>

        <div style="display:flex;gap:12px;align-items:center">
          <div style="font-weight:700">Pinned repos</div>
          <div style="opacity:0.7;font-size:13px">(fetched from top starred)</div>
        </div>

        <div class="repo-list" id="reposRoot">
          <!-- repo cards injected here -->
          <div class="repo">
            <h4>example-repo</h4>
            <p>Small demo repo demonstrating animated profile layout.</p>
            <div class="tag-row"><span class="tag">JavaScript</span><span class="tag">CSS</span></div>
          </div>
        </div>

      </div>
    </div>
  </div>

  <script>
    // Small helper utilities
    const el = (id)=>document.getElementById(id);
    const setText = (id, txt)=>el(id).textContent = txt;

    // Typing animation (subtle) for the name
    function animateTyping(targetId, text){
      const node = el(targetId);
      node.textContent = '';
      let i=0;
      const step = ()=>{
        if(i<=text.length){ node.textContent = text.slice(0,i); i++; setTimeout(step, 40 + Math.random()*50); }
      };
      step();
    }
    animateTyping('typedName','Tajim Ahmed');

    // Load user from GitHub API when username provided
    async function loadGitHub(username){
      if(!username) return setText('bio','No GitHub username provided. Showing local info for Tajim Ahmed.');
      try{
        setText('bio','Loading public GitHub data...');
        const [userRes, repoRes] = await Promise.all([
          fetch(`https://api.github.com/users/${username}`),
          fetch(`https://api.github.com/users/${username}/repos?per_page=100&sort=updated`)
        ]);
        if(!userRes.ok) throw new Error('User not found');
        const user = await userRes.json();
        const repos = await repoRes.json();
        // update avatar
        const avatarRoot = el('avatar');
        avatarRoot.innerHTML = `<img alt="${user.login} avatar" src="${user.avatar_url}?s=600"/>`;
        setText('displayName', user.name || user.login);
        setText('displayRole', (user.bio && user.bio.split('\n')[0]) || 'GitHub user');
        setText('followers', user.followers);
        setText('repos', user.public_repos);
        setText('bio', user.bio || 'A GitHub user without a public bio.');
        animateTyping('typedName', user.name || user.login);

        // pick top 4 repos by stargazers_count
        const top = repos.sort((a,b)=>b.stargazers_count - a.stargazers_count).slice(0,6);
        const root = el('reposRoot'); root.innerHTML='';
        top.forEach(r=>{
          const desc = r.description? r.description : 'No description';
          const langs = r.language? `<span class=\"tag\">${r.language}</span>`: '';
          const html = `<a class=\"repo\" href=\"${r.html_url}\" target=\"_blank\" rel=\"noopener\">\n              <h4>${r.name} <small style=\"opacity:0.7;font-size:12px\">★${r.stargazers_count}</small></h4>\n              <p>${desc}</p>\n              <div class=\"tag-row\">${langs}<span class=\"tag\">Updated ${new Date(r.updated_at).toLocaleDateString()}</span></div>\n            </a>`;
          root.insertAdjacentHTML('beforeend', html);
        });

      }catch(e){
        setText('bio','Could not load GitHub data — ' + e.message);
      }
    }

    // Hook up controls
    el('loadBtn').addEventListener('click', ()=>{
      const u = el('ghUsername').value.trim();
      loadGitHub(u);
    });

    // copy README snippet (markdown) that user can paste into GitHub profile README
    el('copyMd').addEventListener('click', async ()=>{
      const name = el('displayName').textContent || 'Tajim Ahmed';
      const bio = el('bio').textContent || '';
      const md = `# ${name}\n\n${bio}\n\n<!-- Animated profile hero (self-hosted) -->\n<p align=\"center\">\n  <img src=\"https://raw.githubusercontent.com/your-username/your-repo/main/animated-github-profile.png\" alt=\"animated profile\">\n</p>\n`;
      try{ await navigator.clipboard.writeText(md); alert('Markdown snippet copied to clipboard. Paste into your README.md'); }catch(e){ prompt('Copy this markdown:', md); }
    });

    // theme toggle just flips gradient for fun
    el('themeToggle').addEventListener('click', ()=>{
      document.documentElement.style.setProperty('--accent1', Math.random()>0.5? '#ef4444':'#7c3aed');
      document.documentElement.style.setProperty('--accent2', Math.random()>0.5? '#f59e0b':'#06b6d4');
    });

    // small progressive enhancement: load default mocked data (Tajim Ahmed)
    document.addEventListener('DOMContentLoaded', ()=>{
      setText('followers','—'); setText('repos','—');
      // leave initial avatar as initials
    });
  </script>
</body>
</html>



