---
layout: post
title: Desktoday
---

There used to be a mac app on the App Store called Desktoday. Apple removed it eventually due to sandboxing issues. Sad. It still [exists](http://www.hanken.co.uk/desktoday/) technically, but it doesen't work on newer operating systems. The app moved all the files from your desktop and put them in a folder with the day's date. This is the digital equivalent of shoving everything on your desk into your closet and feeling like you have your life together.

_Anyways._ I decided to recreate it in Ruby. Hopefully somebody else will make use of [it](https://github.com/bettinson/desk-today/blob/master/desk-today.rb).

```ruby

#!/usr/bin/env ruby
require 'date'
require "FileUtils"

date = Date.today
desktop = Dir.home() + "/Desktop"
folder_today = Dir.home() +"/Documents/#{date}"
system 'mkdir', '-p', folder_today

Dir.foreach(desktop) do |file|
  if file[0] != '.'  # No hidden files
    FileUtils.move "#{desktop}/#{file}", "#{folder_today}/#{file}"
  end
end
```

#### Update

My friend Erik just informed me that the shell command
```bash
mkdir -p ~/Documents/`date "+%Y-%m-%d"` && mv ~/Desktop/* $_
```

will do the exact same thing. Sigh.
