## String Function
```python
import re
s2 = "The BodyGuard is the best album of 'Whitney Houston'."
# Use the findall() function to find all occurrences of the "st" in the string
result = re.findall("st", s2)
# Print out the list of matched words
Out put: ['st','st']

# Use the split function to split the string by the "\s"
split_array = re.split(r"\s", s2)
# The split_array contains all the substrings, split by whitespace characters
print(split_array)
Out put:
['The', 'BodyGuard', 'is', 'the', 'best', 'album', 'of', "'Whitney", "Houston'."]

Sub function

text = "I have a cat, my cat is cute."
# 将所有的 "cat" 替换成 "dog"
result = re.sub("cat", "dog", text)
print(result)
# 输出: I have a dog, my dog is cute.

text = "我的电话是 138-1234-5678，订单号是 98765。"
# \d+ 是一个正则表达式，表示匹配一个或多个数字
result = re.sub(r"\d+", "", text)
print(result)
# 输出: 我的电话是 --，订单号是 。

phone_number = "13812345678"
# 匹配模式：(138)(\d{4})(5678)
# - (\d{4}) 是一个捕获组，它会捕获中间的4位数字。
# 替换字符串：r"\1****\3"
# - \1 代表第一个捕获组的内容 ("138")
# - \3 代表第三个捕获组的内容 ("5678")
result = re.sub(r"(\d{3})(\d{4})(\d{4})", r"\1****\3", phone_number)
print(result)
# 输出: 138****5678

text = "apple, banana, apple, orange, apple"
# 只将第一个 "apple" 替换为 "grape"
result = re.sub("apple", "grape", text, count=1)
print(result)
# 输出: grape, banana, apple, orange, apple
```
***File***
```python
file = open("/rescourses",'r')
file.name = "path"
file.mode = 'r' / 'w'
file.read()
file.close()
# With syntax
with open("path",'mode') as file
	file_read = file.read()
	file_stuff[0], file_studff[1]......
	Or
	file1 = file.readline(n)
	print(file_read)
# close the file automatically
```