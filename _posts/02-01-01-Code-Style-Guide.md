---
anchor: code_style_guide
---

# কোড স্টাইল গাইড {#code_style_guide_title}

পিএইচপি কমিউনিটি বিশাল ও বৈচিত্র্যময়, যাতে আছে অসংখ্য লাইব্রেরি, ফ্রেমওয়ার্ক এবং অন্যান্য কম্পোনেন্ট। পিএইচপি ডেভেলপাররা সাধারণত এইগুলোর মধ্যে কয়েকটি নির্বাচন করেন এবং একই প্রজেক্টে তাদেরকে সমন্বিতভাবে ব্যাবহার করেন। PHP কোডিং এর ক্ষেত্রে একটি সাধারণ কোড স্টাইল মেনে চলা (যতটুকু সম্ভব) খুবই গুরুত্বপূর্ণ যেন ডেভেলপারেরা তাদের প্রজেক্ট এর জন্য সহজেই বিভিন্ন লাইব্রেরি একত্রিত করে ও তাদের সমন্বয় করে কাজ করতে পারেন।

[Framework Interop Group][fig] এর দ্বারা প্রস্তাবিত এবং অনুমোদিত কিছু নীতিমালা আছে। এর সবগুলোই কোড স্টাইল সম্পর্কিত নয়, যেগুলো এ সম্পর্কিত সেগুলো হল [PSR-0][psr0], [PSR-1][psr1], [PSR-2][psr2] এবং [PSR-4][psr4]। এই নীতিমালাগুলো কেবল কিছু নিয়মের সমন্বয় যেগুলো Drupal, Zend, Symfony, Laravel, CakePHP, phpBB, AWS SDK, FuelPHP, Lithium ইত্যাদি প্রজেক্টও মেনে চলে। যে কেউ ইচ্ছা করলে তার প্রজেক্টে এই নিয়মগুলোও মেনে চলতে পারে অথবা তার নিজস্ব স্টাইলও মেনে চলতে পারে।

কোন একটি প্রচলিত নিয়ম অনুসরণ করে পিএইচপি কোড লিখা উচিৎ। তা হতে পারে কতগুলো PSR এর সমন্বয় অথবা PEAR বা Zend এর তৈরিকৃত কোন মানদণ্ড। অর্থাৎ অন্যান্য ডেভেলপারেরা যেন সহজেই আপনার কোড পড়তে পারে ও এটি নিয়ে কাজ করতে পারে এবং যেসব অ্যাপ্লিকেশন্স কম্পোনেন্টগুলোকে ইমপ্লিমেন্ট করে তাদের মাঝেও যেন সামঞ্জস্যতা থাকে এমনকি যখন অসংখ্য থার্ড-পার্টি কোড নিয়ে কাজ করা হয়।

* [PSR-0 সম্বন্ধে জানুন][psr0]
* [PSR-1 সম্বন্ধে জানুন][psr1]
* [PSR-2 সম্বন্ধে জানুন][psr2]
* [PSR-4 সম্বন্ধে জানুন][psr4]
* [PEAR কোডিং স্ট্যান্ডার্ডস সম্বন্ধে জানুন][pear-cs]
* [Symfony কোডিং স্ট্যান্ডার্ডস সম্বন্ধে জানুন][symfony-cs]

উপরোক্ত নিয়মগুলোর বিপরীতে কোড চেক করার জন্য [PHP_CodeSniffer][phpcs] ব্যবহার করা যেতে পারে এবং বিভিন্ন টেক্সট এডিটর, যেমন [Sublime Text][st-cs] এর প্লাগইনস ব্যবহার করা যেতে পারে যেটি রিয়েল-টাইম ফিডব্যাক প্রদর্শন করে।

নিচের যেকোন একটি টুলস ব্যবহার করে স্বয়ংক্রিয়ভাবে কোড লেআউট ঠিক করা যায়ঃ

- একটি হল [PHP Coding Standards Fixer][phpcsfixer] যার কোডবেস খুব ভালোভাবে Tested ।
- এছাড়াও আছে [PHP Code Beautifier and Fixer][phpcbf] যেটি PHP_CodeSniffer এর সাথেই দেয়া থাকে। এর সাহায্যে কোডকে নিজের পছন্দমত স্টাইল এ সাজানো যায়।

এছাড়াও shell থেকে ম্যানুয়ালি phpcs রান করা যেতে পারেঃ

    phpcs -sw --standard=PSR2 file.php

এটি এররগুলো দেখাবে এবং কিভাবে সেগুলো ঠিক করা যায় তা বিস্তারিতভাবে প্রদর্শন করবে। এটি আরও সহায়ক হতে পারে যদি এই কমান্ড একটি git hook এর মধ্যে অন্তর্ভুক্ত করা হয়। এই পদ্ধতিতে, যেসকল branch এ নির্ধারিত নিয়ম লঙ্ঘন করা হয়েছে সেগুলো ঠিক করার আগে রিপোজিটরিতে প্রবেশ করতে পারবে না।

যদি আপনি PHP_CodeSniffer ব্যবহার করেন, তাহলে এর রিপোর্টকৃত কোড লেআউটের সমস্যাগুলো [PHP Code Beautifier and Fixer][phpcbf] দিয়ে স্বয়ংক্রিয়ভাবে ঠিক করতে পারবেন।

    phpcbf -w --standard=PSR2 file.php

আরেকটি বিকল্প পদ্ধতি হল [PHP Coding Standards Fixer][phpcsfixer] ব্যবহার করা। এটি কোড স্ট্রাকচার ঠিক করার আগে তাতে কি কি সমস্যা ছিল সেগুলো দেখাবে।

    php-cs-fixer fix -v --level=psr2 file.php

সকল ধরণের symbol এর নাম এবং কোডের অবকাঠামোর জন্য ইংরেজিকেই প্রাধান্য দেয়া হয়। কমেন্টস যেকোন ভাষায় লেখা যেতে পারে, যে ভাষা কোডবেস নিয়ে যারা কাজ করছে এবং ভবিষ্যতে যারা কাজ করতে পারে সকলের কাছে সহজে বোধগম্য হয়।


[fig]: http://www.php-fig.org/
[psr0]: http://www.php-fig.org/psr/psr-0/
[psr1]: http://www.php-fig.org/psr/psr-1/
[psr2]: http://www.php-fig.org/psr/psr-2/
[psr4]: http://www.php-fig.org/psr/psr-4/
[pear-cs]: http://pear.php.net/manual/en/standards.php
[symfony-cs]: http://symfony.com/doc/current/contributing/code/standards.html
[phpcs]: http://pear.php.net/package/PHP_CodeSniffer/
[phpcbf]: https://github.com/squizlabs/PHP_CodeSniffer/wiki/Fixing-Errors-Automatically
[st-cs]: https://github.com/benmatselby/sublime-phpcs
[phpcsfixer]: http://cs.sensiolabs.org/
