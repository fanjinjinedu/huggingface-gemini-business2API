🚀 HuggingFace Gemini Business 2API

<div align="center">

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=flat-square&logo=huggingface&logoColor=black)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=flat-square&logo=google-bard&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

**无需繁琐配置，无需重复部署。**
**一键提取 Key，轻松将 Gemini Business 转化为标准 API 使用。**

[部署教程](#-部署步骤) • [获取 Key](#-获取-api-key) • [客户端配置](#-客户端配置-cherry-studio)

</div>

---

## ✨ 项目特点

*   **极简部署**：只需在 Hugging Face 上传 4 个文件，无需配置任何环境变量。
*   **Docker 驱动**：基于 Docker 容器，稳定高效。
*   **一键提取**：配合专属油猴脚本，自动生成“终极 API Key”，包含所有动态验证参数。
*   **兼容性强**：生成的 API 支持 Cherry Studio 等常见 AI 客户端。

---

## 🛠️ 部署步骤

在 Hugging Face 上部署只需简单几步：

1.  **创建 Space**：
    *   点击 Create new Space。
    *   **SDK** 选择 `Docker`。
    *   **Space Hardware** 选择默认免费配置即可。

2.  **上传核心文件**：
    在该 Space 的 `Files` 页面，直接上传本项目中的以下 4 个文件：
    *   📄 `docker-compose.yml`
    *   📄 `requirements.txt`
    *   📄 `main.py`
    *   📄 `Dockerfile`

3.  **等待构建**：包含上述文件后，Space 会自动开始构建。显示 "Running" 即部署成功。

> ✅ **注意**：本项目**无需**在 Space Settings 中添加任何 Secret 或 Variable。

---

## 🔑 获取 API Key

使用配套的油猴（Tampermonkey）脚本，一键从 Gemini Business 网页版提取可用 Key。

### 1. 安装脚本
请在 Tampermonkey 中添加新脚本，代码如下（点击展开复制）：

<details>
<summary><strong>👇 点击查看/复制油猴脚本代码</strong></summary>

```javascript
// ==UserScript==
// @name         Gemini Business 2API Helper (v1.2 Ultimate)
// @namespace    https://linux.do/u/f-droid
// @version      1.2
// @icon         https://cdn.inviter.co/community/b5c3dc29-b7e3-49f9-a18d-819398ba4fe6.png
// @description  提取 Gemini Business 配置，生成包含所有动态变量的终极 API Key。
// @author       Gemini Business
// @match        https://business.gemini.google/*
// @grant        GM_setClipboard
// @grant        GM_addStyle
// @grant        GM_cookie
// @connect      business.gemini.google
// ==/UserScript==

(function() {
    'use strict';
    const getFavicon = () => {
        const link = document.querySelector("link[rel*='icon']") || document.querySelector("link[rel='shortcut icon']");
        return link ? link.href : 'https://cdn.inviter.co/community/b5c3dc29-b7e3-49f9-a18d-819398ba4fe6.png';
    };
    GM_addStyle(`:root{--gb-primary:#1a73e8;--gb-primary-hover:#1557b0;--gb-success:#1e8e3e;--gb-success-hover:#137333;--gb-surface:#fff;--gb-bg:#f8f9fa;--gb-text-main:#202124;--gb-text-sub:#5f6368;--gb-border:#dadce0;--gb-shadow-sm:0 1px 2px 0 rgba(60,64,67,.3),0 1px 3px 1px rgba(60,64,67,.15);--gb-shadow-md:0 4px 8px 3px rgba(60,64,67,.15),0 1px 3px rgba(60,64,67,.3);--gb-shadow-lg:0 8px 24px rgba(60,64,67,.2);--gb-font:'Google Sans','Roboto',Arial,sans-serif;--gb-mono:'Roboto Mono','Menlo',monospace;--transition:all .2s cubic-bezier(.4,0,.2,1)}#gb-float-ball{position:fixed;bottom:32px;right:32px;width:60px;height:60px;background:#fff;border-radius:50%;box-shadow:0 4px 16px rgba(0,0,0,.12);cursor:pointer;z-index:9998;border:1px solid var(--gb-border);display:flex;align-items:center;justify-content:center;transition:var(--transition);transform:scale(1)}#gb-float-ball:hover{transform:scale(1.1) rotate(10deg);box-shadow:0 8px 24px rgba(0,0,0,.18)}#gb-float-ball img{width:36px;height:36px;border-radius:8px;object-fit:contain;pointer-events:none}#gb-float-ball::after{content:'Key';position:absolute;bottom:-4px;right:-4px;font-size:8px;font-weight:700;background:var(--gb-primary);color:#fff;padding:2px 6px;border-radius:8px;transform:rotate(-15deg)}#gb-overlay{position:fixed;inset:0;background:rgba(32,33,36,.6);backdrop-filter:blur(3px);z-index:9999;display:flex;align-items:center;justify-content:center;opacity:0;pointer-events:none;transition:opacity .25s ease}#gb-overlay.active{opacity:1;pointer-events:auto}#gb-panel{width:520px;max-width:90vw;background:var(--gb-surface);border-radius:24px;box-shadow:var(--gb-shadow-lg);overflow:hidden;display:flex;flex-direction:column;transform:scale(.92) translateY(20px);transition:transform .3s cubic-bezier(.2,0,0,1);font-family:var(--gb-font)}#gb-overlay.active #gb-panel{transform:scale(1) translateY(0)}.gb-header{background:linear-gradient(135deg,#4285f4 0%,#34a853 100%);padding:24px 32px;color:#fff}.gb-title{font-size:22px;font-weight:500;margin:0;letter-spacing:.5px}.gb-subtitle{font-size:13px;opacity:.9;margin-top:6px;font-weight:400}.gb-body{padding:24px 32px 16px;background:var(--gb-surface)}.gb-label{font-size:14px;color:var(--gb-text-sub);margin-bottom:12px;font-weight:500;display:flex;justify-content:space-between;align-items:center}.gb-textarea-wrapper{position:relative;border:1px solid var(--gb-border);border-radius:12px;background:var(--gb-bg);transition:border-color .2s,background .2s}.gb-textarea-wrapper.editing{background:#fff;border-color:var(--gb-primary);box-shadow:0 0 0 2px rgba(26,115,232,.2)}.gb-textarea{width:100%;height:140px;border:none;background:0 0;padding:16px;font-family:var(--gb-mono);font-size:13px;line-height:1.6;color:var(--gb-text-main);resize:none;outline:none;box-sizing:border-box;word-break:break-all}.gb-status{margin-top:12px;font-size:13px;display:flex;align-items:center;gap:8px;color:var(--gb-text-sub);height:20px}.gb-dot{width:8px;height:8px;border-radius:50%;background:#ccc;transition:background .3s}.gb-dot.success{background:var(--gb-success)}.gb-dot.error{background:#ea4335}.gb-footer{padding:16px 32px 24px;display:flex;justify-content:flex-end;gap:12px;border-top:1px solid #f1f3f4;background:var(--gb-surface)}.gb-btn{border:none;outline:none;padding:0 24px;height:40px;border-radius:20px;font-family:var(--gb-font);font-size:14px;font-weight:500;cursor:pointer;transition:all .2s;display:flex;align-items:center;justify-content:center}.gb-btn-text{background:0 0;color:var(--gb-text-sub)}.gb-btn-text:hover{background:rgba(0,0,0,.05);color:var(--gb-text-main)}.gb-btn-primary{background:var(--gb-primary);color:#fff;box-shadow:var(--gb-shadow-sm)}.gb-btn-primary:hover{background:var(--gb-primary-hover);box-shadow:var(--gb-shadow-md)}.gb-btn-primary:active{transform:scale(.98)}.gb-btn-success{background:var(--gb-success);color:#fff}.gb-btn-success:hover{background:var(--gb-success-hover)}.gb-hidden{display:none!important}`);
    const floatBall=document.createElement("div");floatBall.id="gb-float-ball";floatBall.title="提取 API Key";const ballIcon=document.createElement("img");ballIcon.src=getFavicon();floatBall.appendChild(ballIcon);document.body.appendChild(floatBall);const overlay=document.createElement("div");overlay.id="gb-overlay";const panel=document.createElement("div");panel.id="gb-panel";overlay.appendChild(panel);document.body.appendChild(overlay);const header=document.createElement("div");header.className="gb-header";const title=document.createElement("h2");title.className="gb-title";title.textContent="Gemini Business 2API Helper";const subtitle=document.createElement("div");subtitle.className="gb-subtitle";subtitle.textContent="一键提取终极 API Key";header.appendChild(title);header.appendChild(subtitle);panel.appendChild(header);const body=document.createElement("div");body.className="gb-body";const label=document.createElement("div");label.className="gb-label";label.textContent="生成的 API Key (直接复制使用):";body.appendChild(label);const textWrapper=document.createElement("div");textWrapper.className="gb-textarea-wrapper";const textarea=document.createElement("textarea");textarea.className="gb-textarea";textarea.readOnly=!0;textarea.spellcheck=!1;textWrapper.appendChild(textarea);body.appendChild(textWrapper);const statusDiv=document.createElement("div");statusDiv.className="gb-status";const statusDot=document.createElement("div");statusDot.className="gb-dot";const statusText=document.createElement("span");statusText.textContent="等待操作...";statusDiv.appendChild(statusDot);statusDiv.appendChild(statusText);body.appendChild(statusDiv);panel.appendChild(body);const footer=document.createElement("div");footer.className="gb-footer";const btnClose=document.createElement("button");btnClose.className="gb-btn gb-btn-text";btnClose.textContent="关闭";const btnCopy=document.createElement("button");btnCopy.className="gb-btn gb-btn-primary";btnCopy.textContent="复制 Key";footer.appendChild(btnClose);footer.appendChild(btnCopy);panel.appendChild(footer);let extractedData="";const setStatus=(e,t)=>{statusDot.className="gb-dot "+("success"===e?"success":"error"===e?"error":""),statusText.textContent=t};const openPanel=()=>{overlay.classList.add("active"),textarea.value="正在读取环境数据...",textarea.style.color="#9aa0a6",btnCopy.disabled=!0,setStatus("normal","分析中...");const e=window.location.pathname.split("/"),t=e.indexOf("cid"),o=t!==-1&&e.length>t+1?e[t+1]:null,s=new URLSearchParams(window.location.search).get("csesidx");GM_cookie("list",{},(e,t)=>{if(t)return textarea.value="错误：无法读取 Cookie。\n请检查 Tampermonkey 权限。",textarea.style.color="#ea4335",void setStatus("error","读取失败");const a=(e.find(e=>"__Host-C_OSES"===e.name&&e.domain===window.location.hostname)||{}).value||"",n=(e.find(e=>"__Secure-C_SES"===e.name)||{}).value||null;if(!o||!n||!s)return textarea.value="⚠️ 数据不完整。\n请确保您在 Gemini Business 聊天界面，且 URL 包含 /cid/ 和 ?csesidx=",textarea.style.color="#f9ab00",void setStatus("error","数据缺失");extractedData=`${o}#${n}#${a}#${s}`,textarea.value=extractedData,textarea.style.color="var(--gb-text-main)",btnCopy.disabled=!1,setStatus("success","Key 提取成功")})};const closePanel=()=>{overlay.classList.remove("active")};const copyToClipboard=()=>{textarea.value&&(GM_setClipboard(textarea.value),btnCopy.textContent="已复制",btnCopy.classList.remove("gb-btn-primary"),btnCopy.classList.add("gb-btn-success"),setTimeout(()=>{btnCopy.textContent="复制 Key",btnCopy.classList.remove("gb-btn-success"),btnCopy.classList.add("gb-btn-primary"),closePanel()},1200))};floatBall.addEventListener("click",openPanel),btnClose.addEventListener("click",closePanel),btnCopy.addEventListener("click",copyToClipboard),overlay.addEventListener("click",e=>{e.target===overlay&&closePanel()});
})();
```
</details>

### 2. 提取步骤

1.  打开 [Gemini Business](https://business.gemini.google/)。
2.  进入任意聊天界面。
3.  点击右下角的浮窗按钮（脚本生成）。
4.  在弹出的面板中点击 **"复制 Key"**。

---

## 💻 客户端配置 (Cherry Studio)

以 **Cherry Studio** 为例，配置方式如下：

| 配置项 | 值 / 说明 |
| :--- | :--- |
| **API 密钥** | 使用上方脚本提取得到的 API Key |
| **API 地址** | `https://{HuggingFace用户名}-{项目名称}.hf.space` |
| **模型名称** | 根据实际支持的模型填写 |

> 📌 **提示**：API 地址可以在 Hugging Face Space 页面的右上角菜单 -> "Embed this space" -> "Direct URL" 中找到。通常格式为 `https://user-repo.hf.space`。

---

<img width="100%" alt="Cherry Studio 配置示例" src="https://github.com/user-attachments/assets/530bae42-5044-43da-9e12-24c8babcccfb" />
