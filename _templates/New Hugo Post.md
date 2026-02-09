<%*
const title = await tp.system.prompt("記事のフォルダ名（英語）を入力してください");
if (title) {
    // 常にVaultルートからの絶対パスを指定
    const targetFolder = `content/posts/${title}`;
    const targetPath = `${targetFolder}/index`;

    // 1. フォルダがなければ作成
    if (!app.vault.getAbstractFileByPath(targetFolder)) {
        await app.vault.createFolder(targetFolder);
    }

    // 2. 現在のファイルを強制的にその場所へ移動（リネーム）
    // これにより、ルートに作成された「無題」ファイルが即座に移動されます
    await tp.file.move(targetPath);
}
%>---
title: "<%* tR += title %>"
date: <% tp.date.now("YYYY-MM-DDTHH:mm:ssZ") %>
draft: true
---

# <%* tR += title %>

<% tp.file.cursor() %>