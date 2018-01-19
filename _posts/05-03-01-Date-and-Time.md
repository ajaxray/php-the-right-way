---
title:   Date and Time
isChild: true
anchor:  date_and_time
---

## তারিখ ও সময় {#date_and_time_title}

PHP তে DateTime নামে একটি ক্লাস আছে যা আপনাকে তারিখ ও সময় এর ইনপুট, আউটপুট, তুলনা করা অথবা অন্যান্য হিসাব-নিকাশ এর কাজে সাহায্য করবে। যদিও PHP তে DateTime ক্লাস ছাড়াও তারিখ ও সময় সম্পর্কিত অন্যান্য অনেক ফাংশন রয়েছে, কিন্তু সাধারণভাবে ব্যবহারের ক্ষেত্রে এটি মানসম্মত অবজেক্ট ওরিয়েন্টেড ইন্টারফেস প্রদান করে। এই ক্লাস টাইম জোন নিয়েও কাজ করতে পারে, তবে এখানে তা বিস্তারিতভাবে উল্লেখ করা হলো না।

DateTime নিয়ে কাজ করার শুরুতে মূল তারিখ ও সময় স্ট্রিং কে `createFromFormat()` ফ্যাক্টরি মেথড দিয়ে একটি অবজেক্ট এ রূপান্তর করতে হয়
অথবা new DateTime এর অবজেক্ট ব্যবহার করে বর্তমান তারিখ ও সময় পাওয়া যায় এবং `format()` মেথড ব্যবহার করে পুনরায় এই DateTime কে স্ট্রিং এ রূপান্তর করা যায়।

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('Y-m-d') . "\n";
{% endhighlight %}

DateTime ক্লাসের সাথে DateInterval ক্লাস ব্যবহার করে তারিখ ও সময় হিসেব করা সম্ভব। DateTime এ `add()` এবং `sub()` নামে মেথড রয়েছে যা DateInterval এর অবজেক্ট  কে আর্গুমেন্ট হিসেবে গ্রহণ করে। ডেলাইট সেভিং এবং টাইমজোন ভিন্নতার কারনে দিনের সময়কে সমান সংখ্যক সেকেন্ড ধরে কোড লেখা ঠিক নয়। এক্ষেত্রে DateInterval ব্যবহার করতে হবে। তারিখ এর পার্থক্য নির্নয়ে `diff()` ব্যবহৃত হয়। এটা DateInterval অবজেক্ট রিটার্ন করে যা খুব সহজে ব্যবহার করা যায়।

{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

DateTime অবজেক্ট ব্যবহার করে আপনি সাধারন তুলনা করতে পারেন:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before the end!\n";
}
{% endhighlight %}

শেষ উদাহরন টি DatePeriod ক্লাস কে বর্ননা করে। এটি পুনরাবৃত্ত ইভেন্টগুলি পুনরাবৃত্তির জন্য ব্যবহার করা হয়। এটি DateTime এর দুটি অবজেক্ট নিতে পারে, শুরু এবং শেষ, এবং ব্যবধান যার জন্য এটি তাদের মধ্যকার সবগুলো ইভেন্ট রিটার্ন করে।

{% highlight php %}
<?php
// output all thursdays between $start and $end
$periodInterval = DateInterval::createFromDateString('first thursday');
$periodIterator = new DatePeriod($start, $periodInterval, $end, DatePeriod::EXCLUDE_START_DATE);
foreach ($periodIterator as $date) {
    // output each date in the period
    echo $date->format('Y-m-d') . ' ';
}
{% endhighlight %}

একটি জনপ্রিয় PHP API এক্সটেনশন হলো [Carbon](http://carbon.nesbot.com)। এটি DateTime ক্লাস এর সকল বৈশিষ্ট ধারন করে, তাই এতে কোড এর পরিবর্তন কম, কিন্তু এতে কিছু অতিরিক্ত বৈশিষ্ট অন্তর্ভুক্ত আছে যেমন, স্থানীয় ভাষায় তারিখ ও সময়, ভিন্ন কিছু পদ্ধতিতে DateTime অবজেক্ট কে যোগ, বিয়োগ এবং ফরম্যাট করা, সেই সাথে আপনার পছন্দসই একটি তারিখ এবং সময় অনুকরণ করে আপনার কোড পরীক্ষা করার উপায়।

* [DateTime সম্পর্কে পড়ুন ][datetime]
* [ডেট ফরমেটিং সম্পর্কে পড়ুন][dateformat] (ডেট এর গ্রহণযোগ্য স্ট্রিং ফরম্যাট)

[datetime]: http://php.net/book.datetime
[dateformat]: http://php.net/function.date
