
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>beforeRunningCommand</key>
	<string>nop</string>
	<key>command</key>
	<string>#!/usr/bin/env ruby18 
$KCODE = 'U'
$char_to_entity = { }
File.open("#{ENV['TM_BUNDLE_SUPPORT']}/entities.txt").read.scan(/^(\d+)\t(.+)$/) do |key, value|
  $char_to_entity[[key.to_i].pack('U')] = value
end
def encode (text)
  text.gsub(/[^\x00-\x7F]|["'&lt;&gt;&amp;]/) do |ch|
    ent = $char_to_entity[ch]
    ent ? "&amp;#{ent};" : sprintf("&amp;#x%02X;", ch.unpack("U")[0])
  end
end
print encode(STDIN.read)
</string>
	<key>fallbackInput</key>
	<string>character</string>
	<key>input</key>
	<string>selection</string>
	<key>keyEquivalent</key>
	<string>@&amp;</string>
	<key>name</key>
	<string>Convert Character / Selection to Entities</string>
	<key>output</key>
	<string>replaceSelectedText</string>
	<key>scope</key>
	<string>text.html</string>
	<key>uuid</key>
	<string>3DD8406C-A116-11D9-A5A2-000D93C8BE28</string>
</dict>
</plist>
