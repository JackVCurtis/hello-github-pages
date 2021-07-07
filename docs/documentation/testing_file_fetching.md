## Can you fetch the contents of a local Javascript file via fetch on Github Pages?

### Let us divine   
<div id="example-js-container"></div>
<script>
fetch("/example.js").then((res) => {
    let result = "";
    let reader = res.body.getReader();
    const decoder = new TextDecoder();
    reader.read().then(function processText({ done, value }) {
        if (value) {
            result += decoder.decode(value)
        }
        if (done) {
            document.getElementById("example-js-container").textContent = result;
        } else {
            return reader.read().then(processText);
        }
    })
});
</script>