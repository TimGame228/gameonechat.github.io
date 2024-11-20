<!doctype html>
<html lang="">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <title>PyWebIO Application</title>
    <meta name="description" content="None">
    <link rel="icon" type="image/png" sizes="32x32" href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQCAYAAAAf8/9hAAAAwklEQVQ4T63TvU5CQRCG4WcwMfEuqOgNtQ2Nd4CxV2LHtVhJ0N7AHdjQUBtrrLwLA4ks2Rx+/Qucw3Y78807M7sz4ft5dq6mI7RQX7o/JCNzfdfetkNifRk6k9wLN9jYdxMkyZPQ1faZXYUwB/OCix8V/W4Y4zJDCsBAX7jdM7iQJY+udELu+cTrP2X/xU2+NMPAg3B3UPaVOOmFoQkapQC8Z8AUpyUBs6MAKrZQ+RErf2PlQTrKKK8gpZdpewgOXOcFTTxEjYwMoIkAAAAASUVORK5CYII=" id="favicon32">
    <link rel="icon" type="image/png" sizes="16x16" href="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAYAAABzenr0AAABmUlEQVRYR82XK0wDQRCGv21TUUUJGBwGDBggGCSGBIcAWnBAgsNAgkKhSMDgCA8HtEXgSDBIDC9DDRgcpoSiKo52yea49DiutMttsz27M/98N7s7OyNo9tujgxSTwDiCIaAXSH27l4AXJA/AFSUuWOajGWnR0ChLP3HWkWSAZEN716CM4JQKW6R5+sunPkCeJJJNBCtAosnAQTMHyS6CDWYoh2mEAxzTR4JzYOCfgYNuBRymmOc5uPAbIMswMS6BbkPBPZkiVSZIc+/X/Qng/vl1C4LXIBzG/JmoAag9hxuDaa+XwAIw6p2JGkCObQSrhtMeLifZYZY1tegCqKsW4zHCadfldqgyqK6oC3DGIZIFXZVI9oIjplkUqArXyatGkYkU1+dc5p0eQY4MghNTqlo6kjkFsI9gScvRlLHkQJDnFhgxpampc6cAikCXpqMp8zcF8AnETSlq6lTaAsD6Flg+hNavofVCZL0UW3+M2uI5VhBWGxIFYL0lUxBWm1KviFttyz0Iq4OJB2F1NPO/qdaG0+DD3qLx/AuMVJFhmC8dSgAAAABJRU5ErkJggg==" id="favicon16">
    <link rel="apple-touch-icon" href="image/apple-touch-icon.png">
    <link rel="manifest" href='data:application/manifest+json,%7B%22name%22%3A%20null%2C%20%22description%22%3A%20null%2C%20%22start_url%22%3A%20%22.%22%2C%20%22display%22%3A%20%22standalone%22%2C%20%22theme_color%22%3A%20%22white%22%2C%20%22background_color%22%3A%20%22white%22%2C%20%22icons%22%3A%20%5B%7B%22src%22%3A%20%22image/apple-touch-icon.png%22%2C%20%22type%22%3A%20%22image/png%22%2C%20%22sizes%22%3A%20%22180x180%22%7D%5D%7D' />
    <link rel="stylesheet" href="css/markdown.min.css">
    <link rel="stylesheet" href="css/codemirror.min.css">
    <link rel="stylesheet" href="css/toastify.min.css">
    <link rel="stylesheet" href="css/bs-theme/default.min.css">
    <link rel="stylesheet" href="css/bootstrap-select.min.css">
    <link rel="stylesheet" href="css/app.css?v=1.8.3">
    
    
</head>
<body class="webio-theme-default">
<div class="pywebio">
    <div class="container no-fix-height" id="output-container">
        <div class="markdown-body" id="markdown-body">
            <div class="text-center" id="pywebio-loading" style="display: none; position: fixed; top: 40%; left: 0;right: 0;">
                <div class="spinner-grow text-info" role="status">
                    <span class="sr-only">Loading...</span>
                </div>
            </div>

            <div id="pywebio-scope-ROOT"></div>
        </div>
        <div id="end-space"></div>

    </div>

    <div id="input-container">
        <div id="input-cards" class="container"></div>
    </div>
</div>

<script src="js/mustache.min.js"></script>  <!--template system-->
<script src="js/codemirror.min.js"></script>  <!--code textarea editor-->
<script src="codemirror/addons.js"></script> <!--codemirror addons: matchbrackets, python mode, active line, auto refresh, mode/meta and loadmode -->
<script src="js/prism.min.js"></script>  <!-- markdown code highlight -->
<script src="js/FileSaver.min.js"></script>  <!-- saving files on the client-side -->
<script src="js/jquery.min.js"></script>
<script src="js/popper.min.js"></script>  <!-- tooltip engine -->
<script src="js/bootstrap.min.js"></script>
<script src="js/toastify.min.js"></script> <!-- toast -->
<script src="js/bs-custom-file-input.min.js"></script> <!-- bootstrap custom file input-->
<script src="js/purify.min.js"></script>  <!-- XSS sanitizer -->
<script src="js/bootstrap-select.min.js"></script>
<script>
    if (window.navigator.userAgent.indexOf('MSIE ') !== -1 || window.navigator.userAgent.indexOf('Trident/') !== -1)
        $('#output-container').html('<div class="alert alert-danger" role="alert"> Sorry, this website does not support IE browser. ☹ </div>');
</script>
<script src="js/pywebio.min.js?v=1.8.3"></script>


<script src="js/require.min.js"></script> <!-- JS module loader -->

<script>
    if (window.WebIO === undefined) { // resource load failed
        let url = new URL(window.location.href);
        if (url.searchParams.get('_pywebio_cdn') === 'false') {
            alert("Failed to load resource")
        } else {
            url.searchParams.set('_pywebio_cdn', 'false');
            window.location.href = url.href;
        }
    }

    require.config({
        paths: {
            'plotly': "https://cdn.plot.ly/plotly-2.12.1.min",
            "ag-grid": "https://unpkg.com/ag-grid-community@28.2.0/dist/ag-grid-community.min",
            "ag-grid-enterprise": "https://unpkg.com/ag-grid-enterprise@28.2.0/dist/ag-grid-enterprise.min",
        },
    });


    $(function () {
        // https://www.npmjs.com/package/bs-custom-file-input
        bsCustomFileInput.init()
    });

    const urlparams = new URLSearchParams(window.location.search);
    WebIO.startWebIOClient({
        output_container_elem: $('#markdown-body'),
        input_container_elem: $('#input-cards'),
        backend_address: urlparams.get('pywebio_api') || '',
        app_name: urlparams.get('app') || 'index',
        protocol: "ws",
        runtime_config: {
            debug: urlparams.get('_pywebio_debug'),
            outputAnimation: !urlparams.get('_pywebio_disable_animate'),
            httpPullInterval: parseInt(urlparams.get('_pywebio_http_pull_interval') || 1000)
        },
    });
</script>



<footer class="footer">
    Powered by <a href="https://www.pyweb.io/" target="_blank">PyWebIO</a>
</footer>
</body>
</html>
