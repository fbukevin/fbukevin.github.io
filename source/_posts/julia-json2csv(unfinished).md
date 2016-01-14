---
layout: post
title: '[Julia] json2csv'
date: 2015-05-25 13:16
comments: true
categories: 
---
用 Python 與 Ruby 都有編碼問題

Ruby 還好一點，但是讀取中文編碼的檔名就有問題了(像我 Windows 系統應該是 Big5，讀取 GBK 的就有問題)

julia> readcsv("") # 預設是 Unicode，就沒有 python 和 ruby 的編碼問題，讀取檔名為中文也可以
julia> writedlm("j.csv", a, ',')  # 這其實就是 writecsv("j.csv", a)，但 delim 必為 ','

發現不要用 .csv，直接用 .txt 然後用 ' ' 隔開，在 excel 中載入時選擇空白分隔就好了

![json.jl.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277291/MFribhlSR8u9yxJZfAi2_json.jl.JPG)
http://julia.readthedocs.org/en/latest/stdlib/io-network/#Base.writecsv
https://github.com/JuliaLang/JSON.jl

julia> Pkg.add("JSON")
julia> import JSON
julia> f = open("file.json", "r")
julia> s = readline(f)
julia> j = JSON.parse(s)
Dict{String,Any} with 5 entries:
  "newest_mids" => {}
  "_id"         => ["\$oid"=>"5563114712cc0e3e1ed725f1"]
  "follows"     => {["uid"=>"3616152072","nickname"=>"反反常常-小小??"],["uid"=>"2548
……
  "uid"         => "1431919253"
  "fans"        => {["uid"=>"5549928463","nickname"=>"腄腄腄腄覺覺毛毛了了同同??"],["uid"=>
……
julia> get(j, "uid", null) 	# get(collection, key, default), 其中 default 是如果找不到要回傳的值
"1431919253"
julia> for c in get(j, "follows", null)
		 println(get(c, "nickname", null))
	   end
...
	   