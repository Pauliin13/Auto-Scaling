
🚀 AWS Auto Scaling Lab (EC2 + ALB + AMI)

<img width="86" height="20" alt="image" src="https://github.com/user-attachments/assets/7c3cccbd-cc48-4ebd-a37c-ed5bd1ea6610" />
<img width="146" height="20" alt="image" src="https://github.com/user-attachments/assets/09a19e66-16ba-4066-a7a3-59286767e9a1" />

[lab175-portfolio.html](https://github.com/user-attachments/files/29392813/lab175-portfolio.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Lab-175 · Auto Scaling na AWS</title>
<link href="https://fonts.googleapis.com/css2?family=Amazon+Ember:wght@400;700&family=Inter:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet" />
<style>
  :root {
    --aws-orange: #FF9900;
    --aws-orange-light: #FFAC31;
    --aws-blue: #232F3E;
    --aws-blue-mid: #1A232F;
    --aws-blue-dark: #0F1923;
    --aws-teal: #00A8D6;
    --aws-green: #1DBF73;
    --aws-red: #E53E3E;
    --aws-gray: #8D99A5;
    --aws-gray-light: #C4CDD4;
    --aws-surface: #1C2B3A;
    --aws-surface-2: #243447;
    --aws-border: #2E4055;
    --text-primary: #EAECEE;
    --text-secondary: #8D99A5;
    --text-muted: #5D707F;
    --font-display: 'Inter', sans-serif;
    --font-mono: 'JetBrains Mono', monospace;
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--font-display);
    background: var(--aws-blue-dark);
    color: var(--text-primary);
    line-height: 1.6;
    font-size: 15px;
  }

  /* ── HEADER ── */
  header {
    background: var(--aws-blue);
    border-bottom: 3px solid var(--aws-orange);
    padding: 0 40px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 56px;
    position: sticky;
    top: 0;
    z-index: 100;
  }

  .header-logo {
    display: flex;
    align-items: center;
    gap: 10px;
  }

  .aws-badge {
    background: var(--aws-orange);
    color: #000;
    font-weight: 700;
    font-size: 12px;
    padding: 2px 8px;
    border-radius: 3px;
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }

  .header-title {
    font-size: 13px;
    color: var(--text-secondary);
    font-weight: 400;
  }

  nav {
    display: flex;
    gap: 24px;
  }

  nav a {
    color: var(--aws-gray-light);
    text-decoration: none;
    font-size: 13px;
    font-weight: 500;
    transition: color 0.2s;
  }

  nav a:hover { color: var(--aws-orange); }

  /* ── HERO ── */
  .hero {
    background: linear-gradient(135deg, var(--aws-blue) 0%, var(--aws-blue-mid) 50%, #0D1F2D 100%);
    padding: 80px 40px 60px;
    position: relative;
    overflow: hidden;
  }

  .hero::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse 60% 80% at 80% 50%, rgba(255,153,0,0.06) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-grid {
    max-width: 1100px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 40px;
    align-items: center;
  }

  .lab-meta {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 20px;
  }

  .lab-tag {
    background: rgba(255,153,0,0.15);
    border: 1px solid rgba(255,153,0,0.4);
    color: var(--aws-orange);
    font-size: 11px;
    font-weight: 600;
    padding: 3px 10px;
    border-radius: 12px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }

  .lab-num {
    color: var(--text-muted);
    font-size: 12px;
    font-family: var(--font-mono);
  }

  .hero h1 {
    font-size: clamp(28px, 4vw, 44px);
    font-weight: 700;
    line-height: 1.15;
    letter-spacing: -0.02em;
    margin-bottom: 16px;
  }

  .hero h1 span { color: var(--aws-orange); }

  .hero-desc {
    color: var(--text-secondary);
    font-size: 16px;
    max-width: 560px;
    line-height: 1.7;
    margin-bottom: 32px;
  }

  .hero-stats {
    display: flex;
    gap: 32px;
  }

  .stat {
    display: flex;
    flex-direction: column;
    gap: 3px;
  }

  .stat-value {
    font-size: 22px;
    font-weight: 700;
    color: var(--aws-orange);
    font-family: var(--font-mono);
  }

  .stat-label {
    font-size: 11px;
    color: var(--text-muted);
    text-transform: uppercase;
    letter-spacing: 0.07em;
  }

  /* arch diagram */
  .arch-diagram {
    background: var(--aws-surface);
    border: 1px solid var(--aws-border);
    border-radius: 12px;
    padding: 24px;
    min-width: 280px;
    font-size: 12px;
  }

  .arch-diagram h4 {
    color: var(--aws-gray);
    font-size: 10px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 16px;
    font-weight: 600;
  }

  .arch-flow {
    display: flex;
    flex-direction: column;
    gap: 8px;
    align-items: center;
  }

  .arch-box {
    background: var(--aws-surface-2);
    border: 1px solid var(--aws-border);
    border-radius: 6px;
    padding: 8px 16px;
    font-size: 11px;
    font-weight: 600;
    color: var(--text-primary);
    text-align: center;
    width: 100%;
  }

  .arch-box.orange { border-color: var(--aws-orange); color: var(--aws-orange); }
  .arch-box.teal { border-color: var(--aws-teal); color: var(--aws-teal); }
  .arch-box.green { border-color: var(--aws-green); color: var(--aws-green); }

  .arch-arrow {
    color: var(--text-muted);
    font-size: 14px;
    line-height: 1;
  }

  /* ── MAIN ── */
  main {
    max-width: 1100px;
    margin: 0 auto;
    padding: 60px 40px;
  }

  /* ── SECTION HEADER ── */
  .section-header {
    margin-bottom: 32px;
  }

  .section-label {
    font-size: 11px;
    font-weight: 600;
    color: var(--aws-orange);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: 8px;
  }

  .section-title {
    font-size: 24px;
    font-weight: 700;
    color: var(--text-primary);
    letter-spacing: -0.01em;
  }

  /* ── OBJECTIVES ── */
  .objectives-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 16px;
    margin-bottom: 64px;
  }

  .obj-card {
    background: var(--aws-surface);
    border: 1px solid var(--aws-border);
    border-radius: 10px;
    padding: 20px;
    display: flex;
    gap: 14px;
    align-items: flex-start;
    transition: border-color 0.2s, transform 0.2s;
  }

  .obj-card:hover {
    border-color: rgba(255,153,0,0.4);
    transform: translateY(-2px);
  }

  .obj-icon {
    width: 36px;
    height: 36px;
    border-radius: 8px;
    background: rgba(255,153,0,0.12);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    flex-shrink: 0;
  }

  .obj-text {
    font-size: 13.5px;
    color: var(--text-secondary);
    line-height: 1.55;
  }

  /* ── TASKS ── */
  .tasks { margin-bottom: 64px; }

  .task-block {
    background: var(--aws-surface);
    border: 1px solid var(--aws-border);
    border-radius: 12px;
    overflow: hidden;
    margin-bottom: 20px;
  }

  .task-header {
    display: flex;
    align-items: center;
    gap: 16px;
    padding: 18px 24px;
    background: var(--aws-surface-2);
    border-bottom: 1px solid var(--aws-border);
    cursor: pointer;
    user-select: none;
  }

  .task-num {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: var(--aws-orange);
    color: #000;
    font-weight: 700;
    font-size: 13px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    font-family: var(--font-mono);
  }

  .task-title {
    font-weight: 600;
    font-size: 15px;
    flex: 1;
  }

  .task-time {
    font-size: 11px;
    color: var(--text-muted);
    font-family: var(--font-mono);
    background: var(--aws-blue-dark);
    padding: 2px 8px;
    border-radius: 10px;
  }

  .task-body {
    padding: 24px;
    display: grid;
    gap: 16px;
  }

  .subtask {
    border-left: 2px solid var(--aws-border);
    padding-left: 16px;
  }

  .subtask-title {
    font-size: 12px;
    font-weight: 600;
    color: var(--aws-teal);
    text-transform: uppercase;
    letter-spacing: 0.07em;
    margin-bottom: 10px;
  }

  .step-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 7px;
  }

  .step-list li {
    font-size: 13.5px;
    color: var(--text-secondary);
    line-height: 1.55;
    padding-left: 18px;
    position: relative;
  }

  .step-list li::before {
    content: '›';
    position: absolute;
    left: 0;
    color: var(--aws-orange);
    font-weight: 700;
  }

  .step-list li strong {
    color: var(--text-primary);
    font-weight: 600;
  }

  /* ── CODE BLOCK ── */
  .code-block {
    background: #0B1117;
    border: 1px solid #1E2F3E;
    border-radius: 8px;
    overflow: hidden;
    margin: 12px 0;
  }

  .code-bar {
    background: #111C26;
    padding: 6px 14px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid #1E2F3E;
  }

  .code-lang {
    font-size: 10px;
    color: var(--text-muted);
    font-family: var(--font-mono);
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  .code-dots {
    display: flex;
    gap: 5px;
  }

  .code-dots span {
    width: 8px;
    height: 8px;
    border-radius: 50%;
  }

  .code-dots span:nth-child(1) { background: #FF5F57; }
  .code-dots span:nth-child(2) { background: #FEBC2E; }
  .code-dots span:nth-child(3) { background: #28C840; }

  pre {
    padding: 16px;
    overflow-x: auto;
  }

  code {
    font-family: var(--font-mono);
    font-size: 12.5px;
    line-height: 1.7;
    color: #A8DAAB;
    white-space: pre;
  }

  code .flag { color: #79BCFF; }
  code .str  { color: #FFD580; }
  code .cmt  { color: #4E6374; font-style: italic; }
  code .kw   { color: #C792EA; }

  /* ── ARCHITECTURE SECTION ── */
  .arch-section {
    margin-bottom: 64px;
  }

  .arch-cards {
    display: grid;
    grid-template-columns: 1fr 60px 1fr;
    gap: 0;
    align-items: center;
  }

  .arch-card {
    background: var(--aws-surface);
    border: 1px solid var(--aws-border);
    border-radius: 12px;
    padding: 24px;
  }

  .arch-card h4 {
    font-size: 11px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
    color: var(--aws-gray);
    margin-bottom: 14px;
    font-weight: 600;
  }

  .arch-card ul {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .arch-card li {
    font-size: 13px;
    color: var(--text-secondary);
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .arch-card li::before {
    content: '';
    width: 6px;
    height: 6px;
    border-radius: 50%;
    background: var(--aws-orange);
    flex-shrink: 0;
  }

  .arch-card li.green::before { background: var(--aws-green); }

  .arch-arrow-big {
    text-align: center;
    color: var(--aws-orange);
    font-size: 28px;
    line-height: 1;
  }

  /* ── SERVICES USED ── */
  .services-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    margin-bottom: 64px;
  }

  .service-chip {
    background: var(--aws-surface);
    border: 1px solid var(--aws-border);
    border-radius: 8px;
    padding: 10px 18px;
    font-size: 13px;
    font-weight: 500;
    color: var(--text-primary);
    display: flex;
    align-items: center;
    gap: 8px;
    transition: border-color 0.2s;
  }

  .service-chip:hover { border-color: var(--aws-orange); }

  .service-chip .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--aws-orange);
  }

  /* ── CONCLUSION ── */
  .conclusion {
    background: linear-gradient(135deg, rgba(255,153,0,0.08) 0%, rgba(0,168,214,0.06) 100%);
    border: 1px solid rgba(255,153,0,0.25);
    border-radius: 14px;
    padding: 36px 40px;
    margin-bottom: 40px;
    text-align: center;
  }

  .conclusion h2 {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 12px;
  }

  .conclusion h2 span { color: var(--aws-orange); }

  .conclusion p {
    color: var(--text-secondary);
    max-width: 600px;
    margin: 0 auto 24px;
    line-height: 1.7;
  }

  .achievements {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }

  .badge {
    background: rgba(29,191,115,0.12);
    border: 1px solid rgba(29,191,115,0.3);
    color: var(--aws-green);
    font-size: 12px;
    font-weight: 600;
    padding: 5px 14px;
    border-radius: 20px;
    display: flex;
    align-items: center;
    gap: 6px;
  }

  .badge::before { content: '✓'; }

  /* ── FOOTER ── */
  footer {
    background: var(--aws-blue);
    border-top: 1px solid var(--aws-border);
    padding: 20px 40px;
    text-align: center;
    font-size: 12px;
    color: var(--text-muted);
  }

  footer span { color: var(--aws-orange); }

  /* ── RESPONSIVE ── */
  @media (max-width: 768px) {
    header { padding: 0 20px; }
    nav { display: none; }
    .hero { padding: 48px 20px 40px; }
    .hero-grid { grid-template-columns: 1fr; }
    .arch-diagram { display: none; }
    main { padding: 40px 20px; }
    .arch-cards { grid-template-columns: 1fr; }
    .arch-arrow-big { transform: rotate(90deg); }
  }
</style>
</head>
<body>

<!-- HEADER -->
<header>
  <div class="header-logo">
    <span class="aws-badge">AWS</span>
    <span class="header-title">Hands-on Labs · Portfolio</span>
  </div>
  <nav>
    <a href="#objetivos">Objetivos</a>
    <a href="#tarefas">Tarefas</a>
    <a href="#arquitetura">Arquitetura</a>
    <a href="#servicos">Serviços</a>
    <a href="#conclusao">Conclusão</a>
  </nav>
</header>

<!-- HERO -->
<section class="hero">
  <div class="hero-grid">
    <div>
      <div class="lab-meta">
        <span class="lab-tag">Compute</span>
        <span class="lab-tag">Scalability</span>
        <span class="lab-num">LAB-175</span>
      </div>
      <h1>Auto Scaling<br/>na <span>AWS</span> com Linux</h1>
      <p class="hero-desc">
        Configure uma infraestrutura resiliente e elástica usando EC2, AMIs personalizadas,
        Application Load Balancer e Auto Scaling Groups com políticas de escala automática
        baseadas em utilização de CPU.
      </p>
      <div class="hero-stats">
        <div class="stat">
          <span class="stat-value">45</span>
          <span class="stat-label">Minutos</span>
        </div>
        <div class="stat">
          <span class="stat-value">4</span>
          <span class="stat-label">Tarefas</span>
        </div>
        <div class="stat">
          <span class="stat-value">2</span>
          <span class="stat-label">AZs</span>
        </div>
        <div class="stat">
          <span class="stat-value">50%</span>
          <span class="stat-label">CPU Threshold</span>
        </div>
      </div>
    </div>
    <div class="arch-diagram">
      <h4>Fluxo Final</h4>
      <div class="arch-flow">
        <div class="arch-box orange">Internet / Usuário</div>
        <div class="arch-arrow">↓</div>
        <div class="arch-box teal">Application Load Balancer</div>
        <div class="arch-arrow">↓</div>
        <div class="arch-box">Auto Scaling Group</div>
        <div class="arch-arrow">↓</div>
        <div class="arch-box green">EC2 Instances (2–4)</div>
        <div class="arch-arrow">↓</div>
        <div class="arch-box">Private Subnet AZ-A / AZ-B</div>
      </div>
    </div>
  </div>
</section>

<main>

  <!-- OBJETIVOS -->
  <section id="objetivos">
    <div class="section-header">
      <div class="section-label">O que você vai aprender</div>
      <div class="section-title">Objetivos do Laboratório</div>
    </div>
    <div class="objectives-grid">
      <div class="obj-card">
        <div class="obj-icon">💻</div>
        <div class="obj-text">Criar uma instância <strong>EC2</strong> usando comandos da <strong>AWS CLI</strong></div>
      </div>
      <div class="obj-card">
        <div class="obj-icon">📸</div>
        <div class="obj-text">Criar uma <strong>AMI personalizada</strong> (WebServerAMI) via AWS CLI</div>
      </div>
      <div class="obj-card">
        <div class="obj-icon">📋</div>
        <div class="obj-text">Configurar um <strong>Launch Template</strong> para o EC2 Auto Scaling</div>
      </div>
      <div class="obj-card">
        <div class="obj-icon">⚖️</div>
        <div class="obj-text">Criar um <strong>Application Load Balancer</strong> com target groups e health checks</div>
      </div>
      <div class="obj-card">
        <div class="obj-icon">📈</div>
        <div class="obj-text">Configurar <strong>Auto Scaling Group</strong> com min/max e capacidade desejada</div>
      </div>
      <div class="obj-card">
        <div class="obj-icon">🎯</div>
        <div class="obj-text">Definir <strong>scaling policies</strong> de target tracking baseadas em CPU (50%)</div>
      </div>
    </div>
  </section>

  <!-- ARQUITETURA -->
  <section id="arquitetura" class="arch-section">
    <div class="section-header">
      <div class="section-label">Evolução da Infraestrutura</div>
      <div class="section-title">Arquitetura do Lab</div>
    </div>
    <div class="arch-cards">
      <div class="arch-card">
        <h4>🏗️ Arquitetura Inicial</h4>
        <ul>
          <li>Command Host em Public Subnet</li>
          <li>Acesso via EC2 Instance Connect</li>
          <li>AWS CLI pré-configurada</li>
          <li>Instância WebServer isolada</li>
        </ul>
      </div>
      <div class="arch-arrow-big">→</div>
      <div class="arch-card">
        <h4>🚀 Arquitetura Final</h4>
        <ul>
          <li class="green">Application Load Balancer (público)</li>
          <li class="green">Auto Scaling Group (2–4 instâncias)</li>
          <li class="green">Private Subnet AZ-A e AZ-B</li>
          <li class="green">Health checks e scale-out automático</li>
        </ul>
      </div>
    </div>
  </section>

  <!-- TAREFAS -->
  <section id="tarefas" class="tasks">
    <div class="section-header">
      <div class="section-label">Passo a passo</div>
      <div class="section-title">Tarefas Realizadas</div>
    </div>

    <!-- TAREFA 1 -->
    <div class="task-block">
      <div class="task-header">
        <div class="task-num">1</div>
        <div class="task-title">Criando uma nova AMI para Auto Scaling</div>
        <div class="task-time">~15 min</div>
      </div>
      <div class="task-body">

        <div class="subtask">
          <div class="subtask-title">1.1 · Conectando ao Command Host</div>
          <ul class="step-list">
            <li>Acesse o console da AWS e navegue até <strong>EC2 → Instances</strong></li>
            <li>Selecione a instância <strong>Command Host</strong> e clique em <strong>Connect</strong></li>
            <li>Use o <strong>EC2 Instance Connect</strong> para abrir o terminal no navegador</li>
          </ul>
        </div>

        <div class="subtask">
          <div class="subtask-title">1.2 · Configurando a AWS CLI</div>
          <div class="code-block">
            <div class="code-bar">
              <div class="code-dots"><span></span><span></span><span></span></div>
              <span class="code-lang">bash</span>
            </div>
            <pre><code><span class="cmt"># Descobrir a region atual</span>
curl http://169.254.169.254/latest/dynamic/instance-identity/document | grep region

<span class="cmt"># Configurar credenciais</span>
aws configure
<span class="cmt"># → AWS Access Key ID: Enter</span>
<span class="cmt"># → AWS Secret Access Key: Enter</span>
<span class="cmt"># → Default region name: us-west-2</span>
<span class="cmt"># → Default output format: json</span>

cd /home/ec2-user/</code></pre>
          </div>
        </div>

        <div class="subtask">
          <div class="subtask-title">1.3 · Criando uma instância EC2 via CLI</div>
          <div class="code-block">
            <div class="code-bar">
              <div class="code-dots"><span></span><span></span><span></span></div>
              <span class="code-lang">bash</span>
            </div>
            <pre><code>aws ec2 run-instances \
  <span class="flag">--key-name</span> <span class="str">KEYNAME</span> \
  <span class="flag">--instance-type</span> t3.micro \
  <span class="flag">--image-id</span> <span class="str">AMIID</span> \
  <span class="flag">--user-data</span> file:///home/ec2-user/UserData.txt \
  <span class="flag">--security-group-ids</span> <span class="str">HTTPACCESS</span> \
  <span class="flag">--subnet-id</span> <span class="str">SUBNETID</span> \
  <span class="flag">--associate-public-ip-address</span> \
  <span class="flag">--tag-specifications</span> <span class="str">'ResourceType=instance,Tags=[{Key=Name,Value=WebServer}]'</span> \
  <span class="flag">--output</span> text <span class="flag">--query</span> <span class="str">'Instances[*].InstanceId'</span>

<span class="cmt"># Aguardar a instância ficar running</span>
aws ec2 wait instance-running <span class="flag">--instance-ids</span> <span class="str">NEW-INSTANCE-ID</span>

<span class="cmt"># Obter o Public DNS</span>
aws ec2 describe-instances <span class="flag">--instance-id</span> <span class="str">NEW-INSTANCE-ID</span> \
  <span class="flag">--query</span> <span class="str">'Reservations[0].Instances[0].NetworkInterfaces[0].Association.PublicDnsName'</span></code></pre>
          </div>
        </div>

        <div class="subtask">
          <div class="subtask-title">1.4 · Criando a AMI personalizada</div>
          <div class="code-block">
            <div class="code-bar">
              <div class="code-dots"><span></span><span></span><span></span></div>
              <span class="code-lang">bash</span>
            </div>
            <pre><code>aws ec2 create-image <span class="flag">--name</span> WebServerAMI <span class="flag">--instance-id</span> <span class="str">NEW-INSTANCE-ID</span>
<span class="cmt"># A instância será reiniciada automaticamente durante a criação</span></code></pre>
          </div>
        </div>

      </div>
    </div>

    <!-- TAREFA 2 -->
    <div class="task-block">
      <div class="task-header">
        <div class="task-num">2</div>
        <div class="task-title">Criando o Ambiente de Auto Scaling</div>
        <div class="task-time">~20 min</div>
      </div>
      <div class="task-body">

        <div class="subtask">
          <div class="subtask-title">2.1 · Application Load Balancer</div>
          <ul class="step-list">
            <li>Acesse <strong>EC2 → Load Balancers → Create Load Balancer</strong></li>
            <li>Selecione <strong>Application Load Balancer</strong></li>
            <li>Nome: <strong>WebServerELB</strong> · VPC: <strong>Lab VPC</strong></li>
            <li>Subnets: <strong>Public Subnet 1</strong> e <strong>Public Subnet 2</strong></li>
            <li>Security Group: <strong>HTTPAccess</strong></li>
            <li>Crie o Target Group: tipo <strong>Instances</strong>, nome <strong>webserver-app</strong>, health check em <strong>/index.php</strong></li>
            <li>Em <strong>Forward to</strong>, selecione <strong>webserver-app</strong> e finalize</li>
          </ul>
        </div>

        <div class="subtask">
          <div class="subtask-title">2.2 · Launch Template</div>
          <ul class="step-list">
            <li>Acesse <strong>Launch Templates → Create Launch Template</strong></li>
            <li>Nome: <strong>web-app-launch-template</strong></li>
            <li>Marque a opção de <strong>Auto Scaling guidance</strong></li>
            <li>AMI: <strong>WebServerAMI</strong> · Tipo: <strong>t3.micro</strong> · SG: <strong>HTTPAccess</strong></li>
          </ul>
        </div>

        <div class="subtask">
          <div class="subtask-title">2.3 · Auto Scaling Group</div>
          <ul class="step-list">
            <li>Nome: <strong>Web App Auto Scaling Group</strong></li>
            <li>VPC: <strong>Lab VPC</strong> · Subnets: <strong>Private Subnet 1</strong> e <strong>Private Subnet 2</strong></li>
            <li>Associe ao load balancer <strong>webserver-app | HTTP</strong></li>
            <li>Ative o <strong>Elastic Load Balancing health check</strong></li>
            <li>Capacidade: <strong>Desired: 2 · Min: 2 · Max: 4</strong></li>
            <li>Scaling Policy: <strong>Target Tracking · Average CPU · Valor: 50%</strong></li>
            <li>Tag: <strong>Name = WebApp</strong></li>
          </ul>
        </div>

      </div>
    </div>

    <!-- TAREFA 3 -->
    <div class="task-block">
      <div class="task-header">
        <div class="task-num">3</div>
        <div class="task-title">Verificando o Auto Scaling</div>
        <div class="task-time">~5 min</div>
      </div>
      <div class="task-body">
        <div class="subtask">
          <div class="subtask-title">3.1 · Validação das Instâncias</div>
          <ul class="step-list">
            <li>Aguarde até que as duas instâncias do ASG mostrem status <strong>2/2 checks passed</strong></li>
            <li>Acesse <strong>Target Groups</strong> e confirme status <strong>healthy</strong> para ambas</li>
            <li>Acesse o <strong>DNS do Load Balancer</strong> no navegador para confirmar o funcionamento</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- TAREFA 4 -->
    <div class="task-block">
      <div class="task-header">
        <div class="task-num">4</div>
        <div class="task-title">Testando o Auto Scaling sob Carga</div>
        <div class="task-time">~5 min</div>
      </div>
      <div class="task-body">
        <div class="subtask">
          <div class="subtask-title">4.1 · Stress Test</div>
          <ul class="step-list">
            <li>Acesse o DNS do Load Balancer no navegador</li>
            <li>Clique em <strong>Start Stress</strong> para simular carga elevada</li>
            <li>Vá em <strong>Auto Scaling Group → Activity</strong> e monitore os eventos</li>
            <li>Após alguns minutos, a CPU ultrapassará 50% e uma <strong>nova instância</strong> será provisionada automaticamente</li>
            <li>Confirme a nova instância no painel <strong>EC2 → Instances</strong></li>
          </ul>
        </div>
      </div>
    </div>

  </section>

  <!-- SERVIÇOS -->
  <section id="servicos">
    <div class="section-header">
      <div class="section-label">Stack utilizada</div>
      <div class="section-title">Serviços AWS</div>
    </div>
    <div class="services-grid">
      <div class="service-chip"><span class="dot"></span>Amazon EC2</div>
      <div class="service-chip"><span class="dot"></span>AWS CLI</div>
      <div class="service-chip"><span class="dot"></span>Amazon Machine Image (AMI)</div>
      <div class="service-chip"><span class="dot"></span>EC2 Auto Scaling</div>
      <div class="service-chip"><span class="dot"></span>Application Load Balancer</div>
      <div class="service-chip"><span class="dot"></span>Launch Template</div>
      <div class="service-chip"><span class="dot"></span>Target Group</div>
      <div class="service-chip"><span class="dot"></span>EC2 Instance Connect</div>
      <div class="service-chip"><span class="dot"></span>VPC / Subnets</div>
      <div class="service-chip"><span class="dot"></span>Security Groups</div>
      <div class="service-chip"><span class="dot"></span>CloudWatch (métricas CPU)</div>
    </div>
  </section>

  <!-- CONCLUSÃO -->
  <section id="conclusao" class="conclusion">
    <h2>Laboratório <span>Concluído</span> com Sucesso!</h2>
    <p>
      Você configurou uma infraestrutura elástica e tolerante a falhas na AWS,
      capaz de escalar automaticamente com base na demanda real de CPU,
      distribuindo tráfego por múltiplas zonas de disponibilidade.
    </p>
    <div class="achievements">
      <span class="badge">EC2 via AWS CLI</span>
      <span class="badge">AMI Personalizada</span>
      <span class="badge">Launch Template</span>
      <span class="badge">Application Load Balancer</span>
      <span class="badge">Auto Scaling Group</span>
      <span class="badge">Target Tracking Policy</span>
      <span class="badge">Multi-AZ</span>
    </div>
  </section>

</main>

<footer>
  <p>Lab-175 · Auto Scaling na AWS (Linux) · Portfolio gerado em <span>2025</span></p>
</footer>

</body>
</html>
