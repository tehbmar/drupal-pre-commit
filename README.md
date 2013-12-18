Requirements:
-------------
You need the coder module which you can get with
<strong>$ drush dl coder</strong>

You also need to have a Code Sniffer installed before using this pre-commit script. To install.

1. For Debian-based systems:
 
   <strong>$ sudo apt-get install php-pear</strong>

   For Mac OS:
   
   http://jason.pureconcepts.net/2012/10/install-pear-pecl-mac-os-x/
   
   Or see the general installation guidelines:
   
   http://pear.php.net/manual/en/installation.getting.php
2. <strong>$ sudo pear update-channels<strong>
3. <strong>$ sudo pear install PHP_CodeSniffer-1.4.3 #1.4.3 is needed due to a bug in coder it might be fixed in the dev branch but I haven't checked<strong>
4. <strong>$ sudo ln -sv /path/to/coder/coder_sniffer/Drupal $(pear config-get php_dir)/PHP/CodeSniffer/Standards/Drupal<strong>


Basically, the idea in #4 is to link/include the Drupal's code sniffer module to the standard PHP Code Sniffer. Here is a sample/actual command for #4:

<strong>$ sudo ln -sv /var/www/html/cardcom/sites/all/modules/contrib/coder/coder_sniffer/Drupal/ $(pear config-get php_dir)/PHP/CodeSniffer/Standards/Drupal</strong>

The <strong>$(pear config-get php_dir)</strong> part in the #4 command will be usually evaluated in Ubuntu as <strong>/usr/share/php</strong>

Git Pre-Commit Hook Setup:
------

1. Navigate to {GitRootDir}/.git/hooks
  <br><strong>cd /var/www/html/cardcom/.git/hooks</strong>
2. Symbolically link to pre-commit and prepare-commit-message files
  <br><strong>ln -s /var/www/html/drupal-pre-commit/pre* .</strong>
3. Make sure that the file has an execute permission.
  <br><strong>$ sudo chmod +x pre-commit</strong>
  <br><strong>$ sudo chmod +x prepare-commit-msg</strong>
  
Usage:
--------

The <strong>pre-commit</strong> hook will only run when using <strong>git commit</strong>

If the commit contains any violations of the following type:

0. Checks commit message
1. PHP syntax error
2. PHP coding standard

it will exit before the commit get indexed and will display the offending file(s).

it will display the line of code and the filename that contain bad code. The developer must resolve the problem first in order to stage the commit.

If you're really sure that it is ok to commit the changes without resolving the coding standard problem detected by the script, you can skip or bypass the validation by using <strong>--no-verify</strong>

Ex: <strong>$ git commit -am "#1452 Commit message | Bypassing validation process" --no-verify</strong>


-----------------------------------------------------------------------------------------------------------------------
-----------------------------------------------------------------------------------------------------------------------


<a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US"><img alt="Creative Commons License" style="border-width:0" src="http://i.creativecommons.org/l/by-nc/3.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">Drupal Pre Commit Filter</span> by <span xmlns:cc="http://creativecommons.org/ns#" property="cc:attributionName">Gerald Villorente</span> is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc/3.0/deed.en_US">Creative Commons Attribution-NonCommercial 3.0 Unported License</a>.<br />Based on a work at <a xmlns:dct="http://purl.org/dc/terms/" href="http://www.niden.net/2011/11/git-pre-commit-another-check-to-ensure.html" rel="dct:source">http://www.niden.net/2011/11/git-pre-commit-another-check-to-ensure.html</a>.
