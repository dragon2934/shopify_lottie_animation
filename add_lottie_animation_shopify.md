# step 1
Convert the json file,

for the lottie animation json file, it contains the images file, which is using base64 encode, the format will like this

data:image/jpeg;base64, xxxxxx

that will make the json file too large, when user open the website, it will load the large json file, that make the website slowly.

so first step, we need to convert the json file, here is the PHP
<code>
    <?php
    $json = file_get_contents("xxx.json");

    $data = json_decode($json,true);
    $url = "xxxxx";
    for($i=0;$i<sizeof($data['assets']);$i++){
        $file_name = $data['assets'][$i]['id'].".jpeg";
        $img_data = $data['assets'][$i]['p'];
        $base64_data = explode(",", $img_data);
        file_put_contents($file_name, base64_decode($base64_data[1]));
        $data['assets'][$i]['p'] = $url.$file_name;
    }
    $convert = "xxxxx_convert.json";
    file_put_contents($convert,json_encode($data));
    ?>
</code>

# step 2
upload the converted json file to Shopify store 
<img src="" />



# step 3
add css at the top of the theme.liquid
<code>
#animationWindow {
    width: 100%;
    height: 100%;
}
</code>
# step 4:
add this script at the bottom of the theme.liquid
<code>
<script src='https://cdnjs.cloudflare.com/ajax/libs/bodymovin/5.6.6/lottie.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/gsap/3.3.1/gsap.min.js'></script>
<script src='https://cdnjs.cloudflare.com/ajax/libs/gsap/3.5.1/ScrollTrigger.min.js'></script>
<script src='https://s3-us-west-2.amazonaws.com/s.cdpn.io/35984/ScrollLottie.js'></script>

<script type="text/javascript">

var fileUrl = "{{ 'xxxxxx.json' | asset_url  }}";
ScrollLottie({
 target: '#animationWindow',
 path: fileUrl,
 duration: .1,
 speed: 'medium'
})


</script>
</code>

# step 5:
add custom liquid add the page you want

such as

<img src="" />


If you feel my work help you, please buy me a Coffee! Thanks!

<a href="https://www.buymeacoffee.com/dragon2934g" target="_blank"><img src="https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png" alt="Buy Me A Coffee" style="height: 41px !important;width: 174px !important;box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;-webkit-box-shadow: 0px 3px 2px 0px rgba(190, 190, 190, 0.5) !important;" ></a>
