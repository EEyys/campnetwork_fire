(function() {
  const links = Array.from(document.querySelectorAll('a.secondary-pill-button'));
  if (links.length <= 0) { 
    console.log('链接数量不足4个，无法跳过前三个点击后续');
    return;
  }

  console.log(`找到 ${links.length} 个链接，跳过前三个，从第4个开始每5秒点击一个，最多运行600秒`);

  let index = 0; // 从第4个开始（索引从0开始） 
  const interval = 5000; // 5秒
  const maxDuration = 600000; // 600秒

  const intervalId = setInterval(() => {
    if (index >= links.length) {
      console.log('已经点击完所有后续链接，停止');
      clearInterval(intervalId);
      clearTimeout(timeoutId);
      return;
    }

    const link = links[index];
    const text = link.innerText.trim();

    console.log(`点击第${index + 1}个链接:`, text);
    link.click();

    if (text === 'Go to X') {
      console.log(`再次点击第${index + 1}个链接（文本为 "Go to X"）`);
      setTimeout(() => link.click(), 200); // 延迟 1000ms 再点一次 
    }

    index++;
  }, interval);

  const timeoutId = setTimeout(() => {
    console.log('达到最大运行时间600秒，停止点击');
    clearInterval(intervalId);
  }, maxDuration);
})();
