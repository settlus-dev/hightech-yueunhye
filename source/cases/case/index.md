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
  #smarteditor-view p.se-text-paragraph {
    margin: 0;
  }
  #contents-omit {
    position: relative;
    padding: 0 0 100px;
    text-align: center;
  }
  #contents-omit:before {
    content: "";
    display: block;
    position: absolute;
    right: 0;
    bottom: 100%;
    left: 0;
    height: 200px;
    background: linear-gradient(0deg, rgba(255,255,255,1) 0%, rgba(255,255,255,0) 100%);
  }
  #contents-omit a {
    display: inline-block;
    padding: 15px 40px;
    background-color: var(--color-footer-background);
    color: #fff;
    font-size: 20px;
    font-weight: bold;
    text-decoration: none;
  }
</style>
<div id="loading">
  <img src="/images/ui-loading.svg" width="100" alt="">
</div>
<div id="smarteditor-view">
  <!--  -->
</div>
<div id="contents-omit" style="display: none;">
  <a target="_blank">전체글 보기</a>
</div>

<script>
  const postId = window.location.search.split('postId=')[1];
  axios.get(`https://7q4yn3iplb.execute-api.ap-northeast-2.amazonaws.com/blogs/ulive_/posts/${postId}`)
    .then(function (response) {
      const data = response.data;
      const {title, content} = data;
      const $content = $(content);
      const selectCounts = 5;
      const multipleNthSelector = (function () {
        return Array(selectCounts).fill('').map(function (element, index) {
          return ':nth-child(' + (index + 1) + ')';
        }).join(', ');
        // output e.g. - 'nth-child(1), nth-child(2), nth-child(3), ...'
      })();
      const $selectedContent = $content.filter(multipleNthSelector);
      // console.log($selectedContent);
      $('#smarteditor-view').append(`<h2>${title}</h2>`);
      $('#smarteditor-view').append(`<hr>`);
      $('#smarteditor-view').append($selectedContent);
      $('#contents-omit a').attr('href', `https://blog.naver.com/ulive_/${postId}`);
      $('#contents-omit').show();
    })
    .finally((function () {
      $('#loading').remove();
    }));
</script>