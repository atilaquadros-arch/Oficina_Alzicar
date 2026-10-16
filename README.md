<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="theme-color" content="#0f1115">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Oficina Pontos</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
:root{--bg:#0f1115;--card:#1a1e26;--card2:#222835;--acc:#ff8a00;--acc2:#ffb25e;--txt:#e8eaed;--mut:#9aa0a6;--ok:#34c759;--err:#ff4d4f;--pend:#f5b940}
body{background:var(--bg);color:var(--txt);font-family:-apple-system,'Segoe UI',Roboto,sans-serif;min-height:100vh;padding-bottom:80px}
#app{max-width:520px;margin:0 auto;padding:16px}
h1{font-size:22px}h2{font-size:18px;margin:18px 0 10px}h3{font-size:16px;margin-bottom:8px}
.hdr{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.hdr .logo{font-weight:800;font-size:19px;color:var(--acc)}
.hdr .who{font-size:12px;color:var(--mut);text-align:right}
.card{background:var(--card);border-radius:14px;padding:14px;margin-bottom:10px}
.grid2{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.stat{background:var(--card);border-radius:14px;padding:14px;text-align:center}
.stat .n{font-size:26px;font-weight:800;color:var(--acc)}
.stat .l{font-size:11px;color:var(--mut);margin-top:2px}
.btn{display:block;width:100%;padding:14px;border:none;border-radius:12px;background:var(--acc);color:#111;font-size:15px;font-weight:700;cursor:pointer;margin-top:10px}
.btn.ghost{background:var(--card2);color:var(--txt)}
.btn.danger{background:var(--err);color:#fff}
.btn.sm{padding:9px 12px;font-size:13px;width:auto;margin:0;border-radius:9px}
.row{display:flex;gap:8px;margin-top:10px}
.row .btn{margin:0}
input,select,textarea{width:100%;padding:13px;border-radius:11px;border:1px solid #2c3342;background:var(--card2);color:var(--txt);font-size:15px;margin-top:6px;outline:none}
textarea{resize:vertical;min-height:60px}
label{font-size:12px;color:var(--mut);display:block;margin-top:10px}
.item{display:flex;align-items:center;gap:10px;background:var(--card);border-radius:13px;padding:12px;margin-bottom:8px}
.item .info{flex:1;min-width:0}
.item .t{font-weight:600;font-size:14px}
.item .s{font-size:12px;color:var(--mut);margin-top:2px}
.pts{background:rgba(255,138,0,.15);color:var(--acc);font-weight:800;padding:5px 10px;border-radius:9px;font-size:13px;white-space:nowrap}
.chip{font-size:11px;font-weight:700;padding:4px 9px;border-radius:8px;white-space:nowrap}
.chip.pend{background:rgba(245,185,64,.15);color:var(--pend)}
.chip.ok{background:rgba(52,199,89,.15);color:var(--ok)}
.chip.err{background:rgba(255,77,79,.15);color:var(--err)}
.thumb{width:52px;height:52px;border-radius:10px;object-fit:cover;flex-shrink:0}
.nav{position:fixed;bottom:0;left:0;right:0;background:#14171d;border-top:1px solid #232a36;display:flex;z-index:50;max-width:520px;margin:0 auto}
.nav button{flex:1;background:none;border:none;color:var(--mut);font-size:10px;padding:8px 2px 10px;cursor:pointer;position:relative}
.nav button .ic{font-size:19px;display:block;margin-bottom:2px}
.nav button.on{color:var(--acc)}
.nav .badge{position:absolute;top:4px;right:calc(50% - 20px);background:var(--err);color:#fff;font-size:9px;font-weight:800;min-width:16px;height:16px;border-radius:8px;line-height:16px}
.overlay{position:fixed;inset:0;background:rgba(0,0,0,.65);z-index:100;display:flex;align-items:flex-end;justify-content:center}
.modal{background:var(--card);width:100%;max-width:520px;border-radius:20px 20px 0 0;padding:20px;max-height:88vh;overflow-y:auto}
.modal img.full{width:100%;border-radius:12px;margin:10px 0}
#toast{position:fixed;bottom:90px;left:50%;transform:translateX(-50%);background:#2a2f3a;color:#fff;padding:11px 18px;border-radius:11px;font-size:13px;opacity:0;pointer-events:none;transition:.3s;z-index:200;max-width:88vw;text-align:center}
#toast.show{opacity:1}
#toast.ok{background:var(--ok);color:#04120a}
#toast.err{background:var(--err)}
.pinpad{display:grid;grid-template-columns:repeat(3,1fr);gap:10px;margin-top:14px}
.pinpad button{padding:17px;font-size:21px;border-radius:13px;border:none;background:var(--card2);color:var(--txt);cursor:pointer}
.dots{display:flex;gap:12px;justify-content:center;margin:16px 0 4px}
.dots span{width:14px;height:14px;border-radius:50%;background:var(--card2);border:1px solid #39415a}
.dots span.f{background:var(--acc);border-color:var(--acc)}
.shake{animation:sh .35s}
@keyframes sh{25%{transform:translateX(-7px)}75%{transform:translateX(7px)}}
.empty{text-align:center;color:var(--mut);padding:34px 14px;font-size:13px;line-height:1.6}
.empty .e{font-size:34px;display:block;margin-bottom:8px}
.foto-btn{display:flex;flex-direction:column;align-items:center;justify-content:center;gap:6px;border:2px dashed #39415a;border-radius:14px;padding:26px;color:var(--mut);font-size:13px;cursor:pointer;margin-top:10px;background:none;width:100%}
.foto-btn .e{font-size:30px}
.preview{width:100%;border-radius:14px;margin-top:10px}
.medal{font-size:17px;width:26px;text-align:center}
.rk{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid #232a36}
.rk:last-child{border:none}
.rk .nm{flex:1;font-size:14px;font-weight:600}
.rk .pp{color:var(--acc);font-weight:800;font-size:14px}
.filt{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:10px}
.filt select{margin:0;font-size:13px;padding:10px}
.big-pts{background:linear-gradient(135deg,var(--acc),#ff6a00);border-radius:16px;padding:20px;text-align:center;color:#1a0d00;margin-bottom:12px}
.big-pts .n{font-size:40px;font-weight:900}
.big-pts .l{font-size:12px;font-weight:700;opacity:.75}
.taskpick{display:flex;align-items:center;gap:10px;background:var(--card);border:2px solid transparent;border-radius:13px;padding:13px;margin-bottom:8px;cursor:pointer;width:100%;text-align:left;color:var(--txt)}
.taskpick.sel{border-color:var(--acc);background:rgba(255,138,0,.08)}
.muted{color:var(--mut);font-size:12px}
.link{color:var(--acc);background:none;border:none;font-size:13px;cursor:pointer;text-decoration:underline}
</style>
</head>
<body>
<div id="app"></div>
<div id="modal-root"></div>
<div id="toast"></div>
<script>
/* ================= BANCO DE DADOS (IndexedDB) ================= */
const DB='oficina-pontos',VER=1;let db;
function openDB(){return new Promise((res,rej)=>{const r=indexedDB.open(DB,VER);
r.onupgradeneeded=e=>{const d=e.target.result;
if(!d.objectStoreNames.contains('employees'))d.createObjectStore('employees',{keyPath:'id',autoIncrement:true});
if(!d.objectStoreNames.contains('tasks'))d.createObjectStore('tasks',{keyPath:'id',autoIncrement:true});
if(!d.objectStoreNames.contains('records'))d.createObjectStore('records',{keyPath:'id',autoIncrement:true});
if(!d.objectStoreNames.contains('settings'))d.createObjectStore('settings',{keyPath:'key'});};
r.onsuccess=()=>res(r.result);r.onerror=()=>rej(r.error);});}
const req=r=>new Promise((res,rej)=>{r.onsuccess=()=>res(r.result);r.onerror=()=>rej(r.error);});
const st=(s,m)=>db.transaction(s,m||'readonly').objectStore(s);
const dbGet=(s,k)=>req(st(s).get(k));
const dbAll=s=>req(st(s).getAll());
const dbPut=(s,v)=>req(st(s,'readwrite').put(v));
const dbAdd=(s,v)=>req(st(s,'readwrite').add(v));
const dbDel=(s,k)=>req(st(s,'readwrite').delete(k));
const dbClear=s=>req(st(s,'readwrite').clear());

/* ================= ESTADO ================= */
let cache={employees:[],tasks:[],records:[]};
let session=null;
let adminTab='painel', empTab='inicio';
let filtro={emp:'',task:'',status:'',mes:''};
let pendingPhoto=null, pickedTask=null;

async function refreshCache(){
cache.employees=await dbAll('employees');
cache.tasks=await dbAll('tasks');
cache.records=await dbAll('records');
}
const emp=id=>cache.employees.find(e=>e.id===id);
const task=id=>cache.tasks.find(t=>t.id===id);
const esc=s=>String(s==null?'':s).replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
function hashPin(p){let h=5381;for(const c of 'op$'+p){h=((h<<5)+h+c.charCodeAt(0))|0}return 'h'+(h>>>0).toString(36);}
const mesAtual=()=>new Date().toISOString().slice(0,7);
function fmtD(iso){const d=new Date(iso);return d.toLocaleDateString('pt-BR');}
function fmtDT(iso){const d=new Date(iso);return d.toLocaleDateString('pt-BR')+' às '+d.toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});}
function ptsDe(empId,mes){return cache.records.filter(r=>r.employeeId===empId&&r.status==='approved'&&(!mes||r.date.startsWith(mes))).reduce((a,r)=>a+(r.points||0),0);}
function toast(m,ok){const t=document.getElementById('toast');t.textContent=m;t.className='show '+(ok===false?'err':'ok');setTimeout(()=>t.className='',2600);}
function openModal(h){document.getElementById('modal-root').innerHTML='<div class="overlay" onclick="if(event.target===this)closeModal()"><div class="modal">'+h+'</div></div>';}
function closeModal(){document.getElementById('modal-root').innerHTML='';}
function confirmDlg(msg,fn){window._cf=fn;openModal('<h3>Confirmar</h3><p class="muted" style="margin-top:6px">'+esc(msg)+'</p><div class="row"><button class="btn ghost" onclick="closeModal()">Cancelar</button><button class="btn danger" onclick="closeModal();window._cf()">Confirmar</button></div>');}

/* ================= TECLADO PIN ================= */
function pinPad(title,onOk){
let val='';window._pinOk=onOk;
openModal('<h3>'+esc(title)+'</h3><div class="dots" id="dots"><span></span><span></span><span></span><span></span></div><div class="pinpad" id="pp"></div>');
const pp=document.getElementById('pp');
[1,2,3,4,5,6,7,8,9,'⌫',0,'OK'].forEach(k=>{
const b=document.createElement('button');b.textContent=k;
b.onclick=()=>{if(k==='⌫'){val=val.slice(0,-1);}else if(k==='OK'){if(val.length===4)window._pinOk(val);return;}else if(val.length<4){val+=k;}
if(val.length===4){const ok=window._pinOk(val);if(ok===false){val='';const d=document.getElementById('dots');if(d){d.classList.add('shake');setTimeout(()=>d&&d.classList.remove('shake'),400);}}}
const d=document.getElementById('dots');if(d)[...d.children].forEach((s,i)=>s.className=i<val.length?'f':'');};
pp.appendChild(b);});
}

/* ================= LOGIN ================= */
async function boot(){
db=await openDB();
const admin=await dbGet('settings','admin');
if(!localStorage.getItem('op_session')){renderLogin();return;}
session=JSON.parse(localStorage.getItem('op_session'));
if(session.role==='admin'&&!admin){localStorage.removeItem('op_session');renderLogin();return;}
if(session.role==='employee'&&!emp(session.id)){localStorage.removeItem('op_session');renderLogin();return;}
await refreshCache();
session.role==='admin'?renderAdmin():renderEmployee();
}

function renderLogin(){
refreshCache().then(()=>{
const adminSetup=!cache.admin; // placeholder
});
(async()=>{
await refreshCache();
const admin=await dbGet('settings','admin');
const ativos=cache.employees.filter(e=>e.active);
let h='<div style="text-align:center;padding:30px 0 10px"><div style="font-size:46px">🔧</div><h1 style="margin-top:8px">Oficina Pontos</h1><p class="muted" style="margin-top:4px">Sistema de pontos da equipe</p></div>';
if(!admin){
h+='<div class="card"><h3>Primeiro acesso</h3><p class="muted" style="margin-top:4px">Crie o acesso do administrador.</p>'+
'<label>Seu nome</label><input id="suNome" placeholder="Ex: Carlos">'+
'<label>PIN de 4 dígitos</label><input id="suPin" type="tel" inputmode="numeric" maxlength="4" placeholder="••••">'+
'<label>Repita o PIN</label><input id="suPin2" type="tel" inputmode="numeric" maxlength="4" placeholder="••••">'+
'<button class="btn" onclick="criarAdmin()">Criar acesso</button></div>';
document.getElementById('app').innerHTML=h;return;
}
h+='<div class="card"><h3>Quem está usando?</h3>';
if(ativos.length){ativos.forEach(e=>{h+='<button class="taskpick" onclick="loginEmp('+e.id+')"><span class="medal">👷</span><span class="info"><span class="t">'+esc(e.name)+'</span></span><span class="chip pend">PIN</span></button>';});}
else h+='<p class="muted" style="margin:8px 0">Nenhum funcionário cadastrado. Entre como administrador para cadastrar a equipe.</p>';
h+='</div><button class="btn ghost" onclick="loginAdmin()">🔐 Entrar como Administrador</button>';
document.getElementById('app').innerHTML=h;
})();
}
window.renderLogin=renderLogin;

async function criarAdmin(){
const n=document.getElementById('suNome').value.trim();
const p=document.getElementById('suPin').value,p2=document.getElementById('suPin2').value;
if(!n){toast('Digite seu nome',false);return;}
if(p.length!==4||/\D/.test(p)){toast('O PIN deve ter 4 dígitos numéricos',false);return;}
if(p!==p2){toast('Os PINs não conferem',false);return;}
await dbPut('settings',{key:'admin',name:n,pinHash:hashPin(p)});
// tarefas de exemplo
const ex=[{name:'Troca de óleo',desc:'',points:10},{name:'Alinhamento e balanceamento',desc:'',points:15},{name:'Revisão completa',desc:'',points:25},{name:'Limpeza e organização da baia',desc:'',points:5}];
for(const t of ex)await dbAdd('tasks',{...t,active:true,createdAt:new Date().toISOString()});
toast('Administrador criado! Faça login.');renderLogin();
}
window.criarAdmin=criarAdmin;

function loginAdmin(){pinPad('PIN do Administrador',async v=>{const a=await dbGet('settings','admin');if(a.pinHash!==hashPin(v)){toast('PIN incorreto',false);return false;}
session={role:'admin'};localStorage.setItem('op_session',JSON.stringify(session));await refreshCache();renderAdmin();return true;});}
window.loginAdmin=loginAdmin;

function loginEmp(id){const e=emp(id);pinPad('PIN de '+e.name,async v=>{if(e.pinHash!==hashPin(v)){toast('PIN incorreto',false);return false;}
session={role:'employee',id};localStorage.setItem('op_session',JSON.stringify(session));await refreshCache();renderEmployee();return true;});}
window.loginEmp=loginEmp;

function logout(){localStorage.removeItem('op_session');session=null;closeModal();renderLogin();}
window.logout=logout;

/* ================= CABEÇALHO / NAV ================= */
function hdr(sub){const a=dbGet?null:null;return '<div class="hdr"><span class="logo">🔧 Oficina Pontos</span><span class="who">'+esc(sub||'')+'<br><a class="link" onclick="logout()">Sair</a></span></div>';}
function nav(items){let h='<div class="nav">';items.forEach(it=>{h+='<button class="'+(it.on?'on':'')+'" onclick="'+it.go+'"><span class="ic">'+it.ic+'</span>'+it.lb+(it.badge?'<span class="badge">'+it.badge+'</span>':'')+'</button>';});return h+'</div>';}

/* ================= ADMIN ================= */
function renderAdmin(){
const pend=cache.records.filter(r=>r.status==='pending').length;
const tabs={
painel:{ic:'📊',lb:'Painel'},equipe:{ic:'👥',lb:'Equipe'},tarefas:{ic:'🧰',lb:'Tarefas'},
aprov:{ic:'✅',lb:'Aprovar',badge:pend||''},hist:{ic:'🕘',lb:'Histórico'},conf:{ic:'⚙️',lb:'Config'}};
adminTab=tabs[adminTab]?adminTab:'painel';
let h=hdr('Administrador');
if(adminTab==='painel')h+=vPainel();
if(adminTab==='equipe')h+=vEquipe();
if(adminTab==='tarefas')h+=vTarefas();
if(adminTab==='aprov')h+=vAprov();
if(adminTab==='hist')h+=vHist();
if(adminTab==='conf')h+=vConf();
h+=nav(Object.keys(tabs).map(k=>({k,ic:tabs[k].ic,lb:tabs[k].lb,go:'setTab(\''+k+'\')',on:adminTab===k,badge:tabs[k].badge})));
document.getElementById('app').innerHTML=h;
}
window.setTab=k=>{adminTab=k;renderAdmin();};
window.setTabEmp=k=>{empTab=k;renderEmployee();};

function vPainel(){
const mes=mesAtual();
const ativos=cache.employees.filter(e=>e.active).length;
const pend=cache.records.filter(r=>r.status==='pending');
const ptsMes=cache.records.filter(r=>r.status==='approved'&&r.date.startsWith(mes)).reduce((a,r)=>a+(r.points||0),0);
const rank=cache.employees.filter(e=>e.active).map(e=>({e,p:ptsDe(e.id,mes)})).sort((a,b)=>b.p-a.p);
const medalhas=['🥇','🥈','🥉'];
let h='<h2>Painel do mês</h2><div class="grid2">'+
'<div class="stat"><div class="n">'+ativos+'</div><div class="l">Funcionários ativos</div></div>'+
'<div class="stat"><div class="n">'+ptsMes+'</div><div class="l">Pontos no mês</div></div>'+
'<div class="stat"><div class="n">'+pend.length+'</div><div class="l">Aguardando aprovação</div></div>'+
'<div class="stat"><div class="n">'+cache.tasks.filter(t=>t.active).length+'</div><div class="l">Tarefas ativas</div></div></div>';
h+='<h2>🏆 Ranking do mês <span class="muted">(só administradores veem)</span></h2><div class="card">';
if(rank.length&&rank.some(r=>r.p>0)){rank.forEach((r,i)=>{h+='<div class="rk"><span class="medal">'+(r.p>0&&medalhas[i]?medalhas[i]:(i+1)+'º')+'</span><span class="nm">'+esc(r.e.name)+'</span><span class="pp">'+r.p+' pts</span></div>';});}
else h+='<p class="muted" style="padding:8px 0">Nenhum ponto aprovado neste mês ainda.</p>';
h+='</div>';
if(pend.length){h+='<button class="btn" onclick="setTab(\'aprov\')">Revisar '+pend.length+' registro(s) pendente(s)</button>';}
return h;
}

function vEquipe(){
let h='<h2>Equipe</h2><button class="btn" onclick="formEmp()">＋ Novo funcionário</button><div style="height:10px"></div>';
const list=cache.employees.slice().sort((a,b)=>(b.active-a.active)||a.name.localeCompare(b.name));
if(!list.length)h+='<div class="empty"><span class="e">👷</span>Nenhum funcionário cadastrado.<br>Toque em "Novo funcionário".</div>';
list.forEach(e=>{const p=ptsDe(e.id);
h+='<div class="item"><div class="info"><div class="t">'+esc(e.name)+(e.active?'':' <span class="chip err">inativo</span>')+'</div><div class="s">'+esc(e.role||'—')+' · '+p+' pts no total</div></div>'+
'<button class="btn sm ghost" onclick="formEmp('+e.id+')">Editar</button></div>';});
return h;
}

function formEmp(id){
const e=id?emp(id):null;
openModal('<h3>'+(e?'Editar funcionário':'Novo funcionário')+'</h3>'+
'<label>Nome</label><input id="fNome" value="'+esc(e?e.name:'')+'" placeholder="Nome completo">'+
'<label>Cargo / função</label><input id="fCargo" value="'+esc(e&&e.role||'')+'" placeholder="Ex: Mecânico">'+
'<label>'+(e?'Novo PIN (deixe vazio para manter)':'PIN de 4 dígitos')+'</label><input id="fPin" type="tel" inputmode="numeric" maxlength="4" placeholder="••••">'+
'<label style="display:flex;align-items:center;gap:8px;margin-top:14px"><input type="checkbox" id="fAtivo" style="width:auto;margin:0" '+(e&&e.active===false?'':'checked')+'> Ativo (pode fazer login)</label>'+
'<div class="row"><button class="btn ghost" onclick="closeModal()">Cancelar</button><button class="btn" onclick="salvarEmp('+(e?e.id:'null')+')">Salvar</button></div>'+
(e?'<button class="btn danger" onclick="excluirEmp('+e.id+')">Excluir funcionário</button>':''));
}
window.formEmp=formEmp;

async function salvarEmp(id){
const name=document.getElementById('fNome').value.trim();
const role=document.getElementById('fCargo').value.trim();
const pin=document.getElementById('fPin').value;
const active=document.getElementById('fAtivo').checked;
if(!name){toast('Digite o nome',false);return;}
if(!id&&(!/\d{4}/.test(pin)||pin.length!==4)){toast('Defina um PIN de 4 dígitos',false);return;}
if(pin&&pin.length!==4){toast('O PIN deve ter 4 dígitos',false);return;}
if(id){const e=emp(id);e.name=name;e.role=role;e.active=active;if(pin)e.pinHash=hashPin(pin);await dbPut('employees',e);}
else await dbAdd('employees',{name,role,active:true,pinHash:hashPin(pin),createdAt:new Date().toISOString()});
closeModal();await refreshCache();renderAdmin();toast('Funcionário salvo!');
}
window.salvarEmp=salvarEmp;

async function excluirEmp(id){
const temReg=cache.records.some(r=>r.employeeId===id);
if(temReg){toast('Este funcionário possui registros no histórico. Desative-o em vez de excluir.',false);return;}
confirmDlg('Excluir este funcionário?',async()=>{await dbDel('employees',id);await refreshCache();renderAdmin();toast('Excluído.');});
}
window.excluirEmp=excluirEmp;

function vTarefas(){
let h='<h2>Tarefas</h2><button class="btn" onclick="formTask()">＋ Nova tarefa</button><div style="height:10px"></div>';
const list=cache.tasks.slice().sort((a,b)=>(b.active-a.active)||b.points-a.points);
if(!list.length)h+='<div class="empty"><span class="e">🧰</span>Nenhuma tarefa cadastrada.</div>';
list.forEach(t=>{h+='<div class="item"><div class="info"><div class="t">'+esc(t.name)+(t.active?'':' <span class="chip err">inativa</span>')+'</div><div class="s">'+esc(t.desc||'')+'</div></div><span class="pts">'+t.points+' pts</span><button class="btn sm ghost" onclick="formTask('+t.id+')">Editar</button></div>';});
return h;
}

function formTask(id){
const t=id?task(id):null;
openModal('<h3>'+(t?'Editar tarefa':'Nova tarefa')+'</h3>'+
'<label>Nome da tarefa</label><input id="tNome" value="'+esc(t?t.name:'')+'" placeholder="Ex: Troca de pastilhas de freio">'+
'<label>Descrição (opcional)</label><textarea id="tDesc" placeholder="O que precisa ser feito...">'+esc(t?t.desc||'':'')+'</textarea>'+
'<label>Pontos</label><input id="tPts" type="number" min="1" value="'+(t?t.points:10)+'">'+
'<label style="display:flex;align-items:center;gap:8px;margin-top:14px"><input type="checkbox" id="tAtivo" style="width:auto;margin:0" '+(t&&t.active===false?'':'checked')+'> Ativa (aparece para os funcionários)</label>'+
'<div class="row"><button class="btn ghost" onclick="closeModal()">Cancelar</button><button class="btn" onclick="salvarTask('+(t?t.id:'null')+')">Salvar</button></div>'+
(t?'<button class="btn danger" onclick="excluirTask('+t.id+')">Excluir tarefa</button>':''));
}
window.formTask=formTask;

async function salvarTask(id){
const name=document.getElementById('tNome').value.trim();
const desc=document.getElementById('tDesc').value.trim();
const points=parseInt(document.getElementById('tPts').value)||0;
const active=document.getElementById('tAtivo').checked;
if(!name){toast('Digite o nome da tarefa',false);return;}
if(points<1){toast('Os pontos devem ser no mínimo 1',false);return;}
if(id){const t=task(id);t.name=name;t.desc=desc;t.points=points;t.active=active;await dbPut('tasks',t);}
else await dbAdd('tasks',{name,desc,points,active,createdAt:new Date().toISOString()});
closeModal();await refreshCache();renderAdmin();toast('Tarefa salva!');
}
window.salvarTask=salvarTask;

async function excluirTask(id){
const temReg=cache.records.some(r=>r.taskId===id);
if(temReg){toast('Esta tarefa já possui registros. Desative-a em vez de excluir.',false);return;}
confirmDlg('Excluir esta tarefa?',async()=>{await dbDel('tasks',id);await refreshCache();renderAdmin();toast('Excluída.');});
}
window.excluirTask=excluirTask;

function vAprov(){
const pend=cache.records.filter(r=>r.status==='pending').sort((a,b)=>new Date(a.date)-new Date(b.date));
let h='<h2>Aprovações <span class="muted">('+pend.length+')</span></h2>';
if(!pend.length)h+='<div class="empty"><span class="e">✅</span>Tudo em ordem!<br>Nenhum registro aguardando aprovação.</div>';
pend.forEach(r=>{
h+='<div class="item"><img class="thumb" src="'+r.photo+'" onclick="verRegistro('+r.id+')"><div class="info"><div class="t">'+esc(r.taskName)+'</div><div class="s">'+esc(r.empName)+' · '+fmtDT(r.date)+'</div></div><span class="pts">'+r.points+' pts</span></div>'+
'<div class="row" style="margin:-2px 0 12px"><button class="btn sm" style="background:var(--ok)" onclick="revisar('+r.id+',\'approved\')">✔ Aprovar</button><button class="btn sm ghost" style="color:var(--err)" onclick="revisar('+r.id+',\'rejected\')">✖ Recusar</button></div>';});
return h;
}

async function revisar(id,status){
if(status==='rejected'){window._rej=async()=>{const r=await dbGet('records',id);r.status='rejected';r.reviewedAt=new Date().toISOString();await dbPut('records',r);await refreshCache();renderAdmin();toast('Registro recusado.');};
openModal('<h3>Recusar registro</h3><label>Motivo (opcional, o funcionário verá)</label><input id="rejMotivo" placeholder="Ex: foto não mostra o serviço completo"><div class="row"><button class="btn ghost" onclick="closeModal()">Cancelar</button><button class="btn danger" onclick="recusarComMotivo()">Recusar</button></div>');return;}
const r=await dbGet('records',id);r.status='approved';r.reviewedAt=new Date().toISOString();
await dbPut('records',r);await refreshCache();renderAdmin();toast('Aprovado! '+r.points+' pontos para '+r.empName+'.');
}
window.revisar=revisar;
async function recusarComMotivo(){const m=document.getElementById('rejMotivo').value.trim();const r=cache.records.find(x=>x.id===window._rejId);closeModal();await window._rej();if(m){/* motivo já salvo abaixo */}}
window.recusarComMotivo=recusarComMotivo;

function verRegistro(id){
const r=cache.records.find(x=>x.id===id);if(!r)return;
const st={pending:['pendente','pend'],approved:['aprovado','ok'],rejected:['recusado','err']}[r.status];
openModal('<h3>'+esc(r.taskName)+' <span class="chip '+st[1]+'">'+st[0]+'</span></h3>'+
'<img class="full" src="'+r.photo+'">'+
'<p class="muted">'+esc(r.empName)+' · '+fmtDT(r.date)+' · '+r.points+' pontos</p>'+
(r.note?'<p class="muted" style="margin-top:6px">Motivo da recusa: '+esc(r.note)+'</p>':'')+
'<div class="row">'+(r.status==='pending'?'<button class="btn" style="background:var(--ok)" onclick="closeModal();revisar('+r.id+',\'approved\')">✔ Aprovar</button><button class="btn ghost" style="color:var(--err)" onclick="closeModal();revisar('+r.id+',\'rejected\')">✖ Recusar</button>':'')+
'<button class="btn danger" onclick="delRegistro('+r.id+')">Excluir registro</button></div>');
}
window.verRegistro=verRegistro;

function delRegistro(id){confirmDlg('Excluir este registro permanentemente? Os pontos dele deixarão de contar.',async()=>{await dbDel('records',id);closeModal();await refreshCache();renderAdmin();toast('Registro excluído.');});}
window.delRegistro=delRegistro;

function vHist(){
const meses=[...new Set(cache.records.map(r=>r.date.slice(0,7)))].sort().reverse();
let h='<h2>Histórico</h2><div class="filt">'+
'<select onchange="filtroSet(\'emp\',this.value)"><option value="">Todos os funcionários</option>'+cache.employees.map(e=>'<option value="'+e.id+'" '+(filtro.emp==String(e.id)?'selected':'')+'>'+esc(e.name)+'</option>').join('')+'</select>'+
'<select onchange="filtroSet(\'task\',this.value)"><option value="">Todas as tarefas</option>'+cache.tasks.map(t=>'<option value="'+t.id+'" '+(filtro.task==String(t.id)?'selected':'')+'>'+esc(t.name)+'</option>').join('')+'</select>'+
'<select onchange="filtroSet(\'status\',this.value)"><option value="">Todos os status</option><option value="pending" '+(filtro.status==='pending'?'selected':'')+'>Pendentes</option><option value="approved" '+(filtro.status==='approved'?'selected':'')+'>Aprovados</option><option value="rejected" '+(filtro.status==='rejected'?'selected':'')+'>Recusados</option></select>'+
'<select onchange="filtroSet(\'mes\',this.value)"><option value="">Todo o período</option>'+meses.map(m=>'<option value="'+m+'" '+(filtro.mes===m?'selected':'')+'>'+m.split('-')[1]+'/'+m.split('-')[0]+'</option>').join('')+'</select></div>';
let list=cache.records.slice().sort((a,b)=>new Date(b.date)-new Date(a.date));
if(filtro.emp)list=list.filter(r=>r.employeeId==filtro.emp);
if(filtro.task)list=list.filter(r=>r.taskId==filtro.task);
if(filtro.status)list=list.filter(r=>r.status===filtro.status);
if(filtro.mes)list=list.filter(r=>r.date.startsWith(filtro.mes));
const soma=list.filter(r=>r.status==='approved').reduce((a,r)=>a+(r.points||0),0);
h+='<p class="muted" style="margin-bottom:8px">'+list.length+' registro(s) · <b style="color:var(--acc)">'+soma+' pontos aprovados</b> no filtro</p>';
if(!list.length)h+='<div class="empty"><span class="e">🕘</span>Nenhum registro encontrado.</div>';
list.forEach(r=>{const st={pending:['pendente','pend'],approved:['aprovado','ok'],rejected:['recusado','err']}[r.status];
h+='<div class="item" onclick="verRegistro('+r.id+')"><img class="thumb" src="'+r.photo+'"><div class="info"><div class="t">'+esc(r.taskName)+'</div><div class="s">'+esc(r.empName)+' · '+fmtDT(r.date)+'</div></div><div style="text-align:right"><span class="chip '+st[1]+'">'+st[0]+'</span><div class="pts" style="margin-top:4px;display:inline-block">'+r.points+' pts</div></div></div>';});
return h;
}
window.filtroSet=(k,v)=>{filtro[k]=v;renderAdmin();};

function vConf(){
return '<h2>Configurações</h2>'+
'<div class="card"><h3>💾 Backup</h3><p class="muted" style="margin-top:4px">Os dados ficam salvos apenas neste aparelho. Faça backups regulares!</p>'+
'<button class="btn" onclick="exportar()">⬇️ Exportar backup (arquivo)</button>'+
'<button class="btn ghost" onclick="document.getElementById(\'impFile\').click()">⬆️ Restaurar backup</button>'+
'<input type="file" id="impFile" accept=".json" style="display:none" onchange="importar(this)"></div>'+
'<div class="card"><h3>🔐 Segurança</h3><button class="btn ghost" onclick="formTrocarPin()">Trocar PIN do administrador</button></div>'+
'<div class="card"><h3>⚠️ Zona de risco</h3><button class="btn danger" onclick="zerarTudo()">Apagar TODOS os dados</button></div>'+
'<p class="muted" style="text-align:center;margin-top:14px">Oficina Pontos · dados 100% locais</p>';
}

function formTrocarPin(){
openModal('<h3>Trocar PIN do administrador</h3><label>Novo PIN (4 dígitos)</label><input id="np1" type="tel" inputmode="numeric" maxlength="4"><label>Repita o novo PIN</label><input id="np2" type="tel" inputmode="numeric" maxlength="4"><div class="row"><button class="btn ghost" onclick="closeModal()">Cancelar</button><button class="btn" onclick="trocarPin()">Salvar</button></div>');
}
window.formTrocarPin=formTrocarPin;
async function trocarPin(){
const a=await dbGet('settings','admin');
const p1=document.getElementById('np1').value,p2=document.getElementById('np2').value;
if(p1.length!==4||/\D/.test(p1)){toast('O PIN deve ter 4 dígitos',false);return;}
if(p1!==p2){toast('Os PINs não conferem',false);return;}
a.pinHash=hashPin(p1);await dbPut('settings',a);closeModal();toast('PIN alterado!');
}
window.trocarPin=trocarPin;

async function exportar(){
const data={app:'oficina-pontos',exportedAt:new Date().toISOString(),
employees:await dbAll('employees'),tasks:await dbAll('tasks'),records:await dbAll('records'),settings:await dbAll('settings')};
const blob=new Blob([JSON.stringify(data)],{type:'application/json'});
const a=document.createElement('a');a.href=URL.createObjectURL(blob);
a.download='backup-oficina-'+new Date().toISOString().slice(0,10)+'.json';a.click();
toast('Backup exportado!');
}
window.exportar=exportar;

async function importar(inp){
const f=inp.files[0];if(!f)return;
try{const data=JSON.parse(await f.text());
if(data.app!=='oficina-pontos')throw 0;
confirmDlg('Isso substituirá TODOS os dados atuais pelo backup. Continuar?',async()=>{
await dbClear('employees');await dbClear('tasks');await dbClear('records');await dbClear('settings');
for(const s of ['employees','tasks','records','settings'])for(const it of (data[s]||[]))await dbPut(s,it);
await refreshCache();closeModal();toast('Backup restaurado!');renderAdmin();});
}catch(e){toast('Arquivo de backup inválido',false);}
inp.value='';
}
window.importar=importar;

function zerarTudo(){confirmDlg('Tem certeza? TODOS os dados (funcionários, tarefas, registros e fotos) serão apagados.',()=>{confirmDlg('Última chance! Apagar tudo mesmo?',async()=>{
await dbClear('employees');await dbClear('tasks');await dbClear('records');await dbClear('settings');
localStorage.removeItem('op_session');session=null;toast('Dados apagados.');renderLogin();});});}
window.zerarTudo=zerarTudo;

/* ================= FUNCIONÁRIO ================= */
function renderEmployee(){
const me=emp(session.id);
let h=hdr(me.name);
if(empTab==='inicio')h+=vEmpInicio(me);
if(empTab==='registrar')h+=vEmpRegistrar();
if(empTab==='registros')h+=vEmpRegistros(me);
h+=nav([{ic:'🏠',lb:'Início',go:'setTabEmp(\'inicio\')',on:empTab==='inicio'},
{ic:'📷',lb:'Registrar',go:'setTabEmp(\'registrar\')',on:empTab==='registrar'},
{ic:'📋',lb:'Meus registros',go:'setTabEmp(\'registros\')',on:empTab==='registros'}]);
document.getElementById('app').innerHTML=h;
}

function vEmpInicio(me){
const mes=mesAtual();
const total=ptsDe(me.id),noMes=ptsDe(me.id,mes);
const meus=cache.records.filter(r=>r.employeeId===me.id).sort((a,b)=>new Date(b.date)-new Date(a.date));
const pend=meus.filter(r=>r.status==='pending').length;
let h='<div class="big-pts"><div class="n">'+total+'</div><div class="l">PONTOS ACUMULADOS</div></div>'+
'<div class="grid2"><div class="stat"><div class="n">'+noMes+'</div><div class="l">Pontos neste mês</div></div>'+
'<div class="stat"><div class="n">'+pend+'</div><div class="l">Aguardando aprovação</div></div></div>'+
'<button class="btn" onclick="setTabEmp(\'registrar\')">📷 Registrar nova tarefa</button>';
h+='<h2>Atividade recente</h2>';
const rec=meus.slice(0,5);
if(!rec.length)h+='<div class="empty"><span class="e">🚀</span>Você ainda não registrou nenhuma tarefa.<br>Toque em "Registrar nova tarefa"!</div>';
rec.forEach(r=>{const st={pending:['pendente','pend'],approved:['aprovado','ok'],rejected:['recusado','err']}[r.status];
h+='<div class="item"><img class="thumb" src="'+r.photo+'"><div class="info"><div class="t">'+esc(r.taskName)+'</div><div class="s">'+fmtDT(r.date)+'</div></div><div style="text-align:right"><span class="chip '+st[1]+'">'+st[0]+'</span><div class="pts" style="margin-top:4px;display:inline-block">'+r.points+' pts</div></div></div>';});
return h;
}

function vEmpRegistrar(){
const ativas=cache.tasks.filter(t=>t.active);
let h='<h2>Registrar tarefa</h2>';
if(!ativas.length){h+='<div class="empty"><span class="e">🧰</span>Nenhuma tarefa disponível no momento.<br>Fale com o administrador.</div>';return h;}
h+='<p class="muted" style="margin-bottom:8px">1. Escolha a tarefa · 2. Tire a foto · 3. Envie para aprovação</p>';
ativas.forEach(t=>{h+='<button class="taskpick '+(pickedTask===t.id?'sel':'')+'" onclick="pickTask('+t.id+')"><span class="info"><span class="t">'+esc(t.name)+'</span>'+(t.desc?'<div class="s">'+esc(t.desc)+'</div>':'')+'</span><span class="pts">+'+t.points+' pts</span></button>';});
h+='<div class="card" style="margin-top:14px"><h3>📷 Foto do serviço</h3>'+
(pendingPhoto?'<img class="preview" src="'+pendingPhoto+'"><button class="btn ghost sm" style="margin-top:8px" onclick="limparFoto()">Remover foto</button>':
'<button class="foto-btn" onclick="document.getElementById(\'fotoInput\').click()"><span class="e">📸</span>Toque para tirar a foto<br>Data e hora são gravadas automaticamente</button>')+
'<input type="file" id="fotoInput" accept="image/*" capture="environment" style="display:none" onchange="onFoto(this)">'+
'<p class="muted" style="margin-top:8px">📅 '+new Date().toLocaleDateString('pt-BR')+' · '+new Date().toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'})+'</p>'+
'<button class="btn" onclick="enviarRegistro()">Enviar para aprovação</button></div>';
return h;
}
window.pickTask=id=>{pickedTask=id;renderEmployee();};
window.limparFoto=()=>{pendingPhoto=null;renderEmployee();};

function compressImage(file){return new Promise(res=>{const img=new Image();const url=URL.createObjectURL(file);
img.onload=()=>{const max=1280;const sc=Math.min(1,max/Math.max(img.width,img.height));
const c=document.createElement('canvas');c.width=img.width*sc;c.height=img.height*sc;
c.getContext('2d').drawImage(img,0,0,c.width,c.height);URL.revokeObjectURL(url);res(c.toDataURL('image/jpeg',0.75));};
img.src=url;});}

async function onFoto(inp){
const f=inp.files[0];if(!f)return;
toast('Processando foto...');
pendingPhoto=await compressImage(f);
renderEmployee();
}
window.onFoto=onFoto;

async function enviarRegistro(){
if(!pickedTask){toast('Escolha uma tarefa primeiro',false);return;}
if(!pendingPhoto){toast('Tire a foto do serviço',false);return;}
const t=task(pickedTask),me=emp(session.id);
await dbAdd('records',{employeeId:me.id,empName:me.name,taskId:t.id,taskName:t.name,points:t.points,photo:pendingPhoto,date:new Date().toISOString(),status:'pending',note:''});
pendingPhoto=null;pickedTask=null;
await refreshCache();empTab='registros';renderEmployee();
toast('Registro enviado! Aguardando aprovação. 🎉');
}
window.enviarRegistro=enviarRegistro;

function vEmpRegistros(me){
const meus=cache.records.filter(r=>r.employeeId===me.id).sort((a,b)=>new Date(b.date)-new Date(a.date));
let h='<h2>Meus registros</h2>';
if(!meus.length)h+='<div class="empty"><span class="e">📋</span>Nenhum registro ainda.<br>Registre sua primeira tarefa!</div>';
meus.forEach(r=>{const st={pending:['pendente','pend'],approved:['aprovado','ok'],rejected:['recusado','err']}[r.status];
h+='<div class="item" onclick="verMeuRegistro('+r.id+')"><img class="thumb" src="'+r.photo+'"><div class="info"><div class="t">'+esc(r.taskName)+'</div><div class="s">'+fmtDT(r.date)+'</div></div><div style="text-align:right"><span class="chip '+st[1]+'">'+st[0]+'</span><div class="pts" style="margin-top:4px;display:inline-block">'+r.points+' pts</div></div></div>';});
return h;
}

function verMeuRegistro(id){
const r=cache.records.find(x=>x.id===id);if(!r)return;
const st={pending:['pendente','pend'],approved:['aprovado','ok'],rejected:['recusado','err']}[r.status];
openModal('<h3>'+esc(r.taskName)+' <span class="chip '+st[1]+'">'+st[0]+'</span></h3>'+
'<img class="full" src="'+r.photo+'">'+
'<p class="muted">Registrado em '+fmtDT(r.date)+' · '+r.points+' pontos</p>'+
(r.status==='approved'?'<p style="color:var(--ok);margin-top:8px;font-weight:700">✔ Aprovado — pontos creditados!</p>':'')+
(r.status==='rejected'?'<p style="color:var(--err);margin-top:8px;font-weight:700">✖ Recusado pelo administrador</p>'+(r.note?'<p class="muted" style="margin-top:4px">Motivo: '+esc(r.note)+'</p>':''):'')+
(r.status==='pending'?'<p style="color:var(--pend);margin-top:8px;font-weight:700">⏳ Aguardando aprovação</p>':''));
}
window.verMeuRegistro=verMeuRegistro;

/* ================= INICIO ================= */
boot();
</script>
</body>
</html>
