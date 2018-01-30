---
isChild: true
anchor:  command_line_interface
---

## কমান্ড লাইন ইন্টারফেইস {#command_line_interface_title}

যদিও পিএইচপি তৈরি করা হয়েছিল ওয়েব অ্যাপ্লিকেশন ডেভেলপ করার জন্য, কিন্তু এটি কমান্ড লাইন ইন্টারফেইস (CLI) প্রোগ্রাম লেখার জন্যও কার্যকর।
কমান্ড লাইন পিএইচপি প্রোগ্রাম টেস্টিং, ডিপ্লয়মেন্ট এবং অ্যাপ্লিকেশন এডমিনিস্ট্রেশন এর মত সাধারণ কাজগুলো স্বয়ংক্রিয় করতে সহায়তা করে।

সিএলআই পিএইচপি প্রোগ্রাম খুবই শক্তিশালী কারণ এর মাধ্যমে আপনি কোন ধরনের web GUI তৈরি করা ও তাকে সিকিউর করা ছাড়াই আপনার অ্যাপ এর কোডকে
ব্যবহার করতে পারেন। তবে খেয়াল রাখতে হবে যে আপনার সিএলআই পিএইচপি স্ক্রিপ্টগুলো যেন আপনার public web root এ **না** রাখা হয়!

কমান্ড লাইন থেকে পিএইচপি রান করুনঃ

{% highlight console %}
> php -i
{% endhighlight %}

`-i` অপশনটি পিএইচপি কনফিগারেশন প্রিন্ট করে দেখাবে যেমনটি [`phpinfo()`][phpinfo] ফাংশন এর মাধ্যমে করা যায়।

`-a` অপশনের মাধ্যমে ইন্টার‍্যাক্টিভ শেল দেখতে পাওয়া যাবে যা রুবির IRB অথবা পাইথন এর ইন্টার‍্যাক্টিভ শেল এর অনুরূপ। এছাড়াও পিএইচপি তে
আরও কিছু প্রয়োজনীয় [কমান্ড লাইন অপশন][cli-options] আছে।

একটি সাধারণ "Hello, $name" সিএলআই প্রোগ্রাম দিয়ে শুরু করা যাক। এটি নিজে নিজে করে দেখতে চাইলে নিচের মত করে `hello.php` নামে একটি ফাইল তৈরি করুন।

{% highlight php %}
<?php
if ($argc !== 2) {
    echo "Usage: php hello.php [name].\n";
    exit(1);
}
$name = $argv[1];
echo "Hello, $name\n";
{% endhighlight %}

আপনার স্ক্রিপ্টটি যে আর্গুমেন্ট দিয়ে রান করা হবে তার উপর ভিত্তি করে পিএইচপি দুটি বিশেষ ভেরিয়েবল সেট করে। [`$argc`][argc] হল একটি ইন্টেজার
ভেরিয়েবল যেখানে আছে আর্গুমেন্ট *count* এবং [`$argv`][argv] হল একটি অ্যারে ভেরিয়েবল যেখানে আছে প্রত্যেকটি আর্গুমেন্ট এর *value*।
প্রথম আর্গুমেন্টটি সবসময় হয় আপনার পিএইচপি স্ক্রিপ্ট ফাইল এর নামে, এক্ষেত্রে `hello.php`।

`exit()` এক্সপ্রেশনটি একটি অশূন্য সংখ্যার সাথে ব্যবহার করা হয় যাতে করে শেল বুঝতে পারে যে কমান্ড ফেইল করেছে। সাধারণভাবে ব্যবহৃত
exit কোডগুলো [এখান][exit-codes] থেকে পেতে পারেন।

উপরের স্ক্রিপ্টটি কমান্ড লাইন থেকে রান করুনঃ

{% highlight console %}
> php hello.php
Usage: php hello.php [name]
> php hello.php world
Hello, world
{% endhighlight %}


 * [কমান্ড লাইন থেকে পিএইচপি রান করা সম্বন্ধে জানুন][php-cli]
 * [উইন্ডোজ এ কমান্ড লাইন থেকে পিএইচপি রান করতে প্রয়োজনীয় সেট আপ সম্বন্ধে জানুন][php-cli-windows]


[phpinfo]: http://php.net/function.phpinfo
[cli-options]: http://php.net/features.commandline.options
[argc]: http://php.net/reserved.variables.argc
[argv]: http://php.net/reserved.variables.argv
[exit-codes]: http://www.gsp.com/cgi-bin/man.cgi?section=3&amp;topic=sysexits
[php-cli]: http://php.net/features.commandline
[php-cli-windows]: http://php.net/install.windows.commandline
