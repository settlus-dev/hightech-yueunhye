---
title: 평가사례
date: 2025-01-17 23:55:52
banner: images/bg-cases.jpg
---

<style>
  #loading {
    margin: 100px 0;
    text-align: center;
  }
  p.se-text-paragraph {
    margin: 0;
  }
</style>
<div id="loading">
  <img src="/images/ui-loading.svg" width="100" alt="">
</div>
<div id="smarteditor-view">
  <!--  -->
</div>

<script>
  const postId = window.location.search.split('postId=')[1];
  axios.get(`https://7q4yn3iplb.execute-api.ap-northeast-2.amazonaws.com/blogs/ulive_/posts/${postId}`)
    .then(function (response) {
      const data = response.data;
      const {title, content} = data;
      $('#smarteditor-view').append(`<h2>${title}</h2>`);
      $('#smarteditor-view').append(`<hr>`);
      $('#smarteditor-view').append(content);
    })
    .finally((function () {
      $('#loading').remove();
    }));
</script>