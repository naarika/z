Common error for all. You just need to add form key to your form. Just add this line below your form declaration.
<input type="hidden" name="form_key" value="<?php echo Mage::getSingleton('core/session')->getFormKey(); ?>" />


http://freaksidea.com/php_and_somethings

<form action="http://localhost/magento/index.php/newsletter/subscriber/new/" method="post" id="newsletter-validate-detail">
        <div class="block-content">
            <div class="form-subscribe-header">
                <label for="newsletter">Sign Up for Our Newsletter:</label>
            </div>
            <div class="input-box">
               <input type="email" autocapitalize="off" autocorrect="off" spellcheck="false" name="email" id="newsletter" title="Sign up for our newsletter" class="input-text required-entry validate-email" />
            </div>
            <div class="actions">
                <button type="submit" title="Subscribe" class="button"><span><span>Subscribe</span></span></button>
            </div>
        </div>
    </form>


CHESS_Frontform
echo ( "<form action=\"http://localhost/magento/index.php/CHESS/Frontform\" method=\"post\" id=\"newsletter-validate-detail\">
        <div class=\"block-content\">
            <div class=\"form-subscribe-header\">
                <label for=\"newsletter\">Sign Up for Our Newsletter:</label>
            </div>
            <div class=\"input-box\">
               <input type=\"email\" autocapitalize=\"off\" autocorrect=\"off\" spellcheck=\"false\" name=\"email\" id=\"newsletter\" title=\"Sign up for our newsletter\" class=\"input-text required-entry validate-email\" />
            </div>
            <div class=\"actions\">
                <button type=\"submit\" title=\"Subscribe\" class=\"button\"><span><span>Subscribe</span></span></button>
            </div>
        </div>
    </form>");
if ($this->getRequest()->isPost() && $this->getRequest()->getPost('email')) {
$email              = (string) $this->getRequest()->getPost('email');
echo "string".$email;
}


<form action="form_handler.php" method=POST> 
<input type="text" name="text" height=300 px width=400px > 
<input type="submit" value="send"> 
</form>

There is a significant difference between the two. $_GET is simply an array, like $_POST. However, calling Mage::app()->getRequest()->getParam('param_name') will give you access to both GET and POST (DELETE and PUT are not included here) - see code below:
lib/Zend/Controller/Request/Http.php

public function getParam($key, $default = null)
{
    $keyName = (null !== ($alias = $this->getAlias($key))) ? $alias : $key;

    $paramSources = $this->getParamSources();
    if (isset($this->_params[$keyName])) {
        return $this->_params[$keyName];
    } elseif (in_array('_GET', $paramSources) && (isset($_GET[$keyName]))) {
        return $_GET[$keyName];
    } elseif (in_array('_POST', $paramSources) && (isset($_POST[$keyName]))) {
        return $_POST[$keyName];
    }

    return $default;
}
In addition, if the system sets other params with Mage::app()->getRequest()->setParam(), it becomes accessible via the getParam() function. In Magento you want to always use getParam().


$getParam = Mage::app()->getRequest()->getParam('getparam');
v
$getParam = $_GET['getparam'];

Magento request

