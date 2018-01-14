---
title:   Date and Time
isChild: true
anchor:  date_and_time
---

## ডেট এন্ড টাইম {#date_and_time_title}

 পিএইচপি তে "DateTime" নামে একটি ক্লাস আছে যা আপনাকে ইনপুট, আউটপুট এবং তুলনা করা এই ধরণের বিভিন্ন কাজে সাহায্য করবে| "DateTime" ক্লাস এর মধ্যে ডেট এবং টাইম সম্পর্কিত অনেক ফাংশন রয়েছে| কিন্তু সাধারণ ব্যবহারের ক্ষেত্রে এটি ভালো মানের অবজেক্ট ওরিয়েন্টেড ইন্টারফেস প্রদান করে| এই ক্লাস টাইমজোন নিয়ে ও কাজ করতে পারে| কিন্তু সংক্ষিপ্ত ভূমিকায় তা উল্লেখ করা হলো না|

DateTime নিয়ে কাজ করার শুরুতে মূল ডেট এবং টাইম স্ট্রিং কে `createFromFormat()` ফ্যাক্টরি মেথড দিয়ে একটি অবজেক্ট এ রূপান্তর করতে হয়
অথবা new DateTime এর অবজেক্ট ব্যবহার করে কারেন্ট ডেট টাইম পাওয়া যায় এবং `format()` মেথড ব্যবহার করে পুনরায় এই DateTime কে স্ট্রিং এ রূপান্তর করা যায়|

{% highlight php %}
<?php
$raw = '22. 11. 1968';
$start = DateTime::createFromFormat('d. m. Y', $raw);

echo 'Start date: ' . $start->format('Y-m-d') . "\n";
{% endhighlight %}

DateTime ক্লাসের সাথে DateInterval ক্লাস ব্যবহার করে ডেট টাইম ক্যালকুলেশন করা যায়| DateTime এ `add()` এবং `sub()` নামে মেথড রয়েছে যা DateInterval এর অবজেক্ট  কে আর্গুমেন্ট হিসেবে গ্রহণ করে| ডেলাইট সেভিং এবং টাইমজোন ভিন্নতার কারনে দিনের সময়কে সমান সংখ্যক সেকেন্ড ধরে কোড লিখা ঠিক নয়| এক্ষেত্রে ডেট ইন্টারবালস ব্যবহার করতে হবে| ডেট এর পার্থক্য নির্নয়ে `diff()` ব্যবহৃত হয়| এটা DateInterval অবজেক্ট রিটার্ন করে যা সহজে ব্যবহার করা যায়|

{% highlight php %}
<?php
// create a copy of $start and add one month and 6 days
$end = clone $start;
$end->add(new DateInterval('P1M6D'));

$diff = $end->diff($start);
echo 'Difference: ' . $diff->format('%m month, %d days (total: %a days)') . "\n";
// Difference: 1 month, 6 days (total: 37 days)
{% endhighlight %}

DateTime অবজেক্ট উপর আপনি গুণগত মানের তুলনা করতে পারেন:

{% highlight php %}
<?php
if ($start < $end) {
    echo "Start is before the end!\n";
}
{% endhighlight %}

 শেষ উদাহরন টি DatePeriod ক্লাস কে বর্ননা করে| এটি পুনরাবৃত্ত ইভেন্টগুলি পুনরাবৃত্তির জন্য ব্যবহার করা হয়| এটি DateTime স্টার্ট এবং এন্ড্ দুইটি অবজেক্ট এবং তাদের মধ্যেকার ব্যবধান গ্রহন করে ও তাদের মধ্যেকার সবগুলো ইভেন্ট রিটার্ন করে|

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

PHP এর একটি জনপ্রিয় API এক্সটেনশন হলো [কার্বন](http://carbon.nesbot.com)| এটি DateTime ক্লাস এর সকল বৈশিষ্ট ধারন করে, তাই এতে কোড এর পরিবর্তন কম, কিন্তু এতে কিছু অতিরিক্ত বৈশিষ্ট অন্তর্ভুক্ত  আছে লোকালাইজেশন সাপোর্ট, পুনরায় যোগ করার উপায়, বিয়োগ করা এবং DateTime অবজেক্ট কে ফরমেট করা এবং আপনার পছন্দসই একটি তারিখ এবং সময় অনুকরণ করে আপনার কোড পরীক্ষা করার উপায়|

 * [DateTime সম্পর্কে পড়ুন ][ডেটটাইম ]
 * [ডেট ফরমেটিং সম্পর্কে পড়ুন][ডেটফরমেট] (ডেট এর গ্রহণযোগ্য স্ট্রিং ফরমেট )

 [ডেটটাইম ]: http://php.net/book.datetime
 [ডেটফরমেট]: http://php.net/function.date
