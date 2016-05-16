# Ruby Cheatsheet

- tags: ruby, cheatsheet, one-line script

------

- Ruby的几个坑
  - #===, #== and #=~
  - a === b 意思大概是b是a类的东西, 具体到每个类对#===的实现上
    - Class#===(obj): obj.is_a?(self)
    - Range#===(obj): obj.member?(self)
    - Regexp#===(obj): self.match(obj)
  - a =~ b的意思是正则表达式匹配
    - Regexp#=~(str), 要求str必须是String, 否则抛出异常TypeError
    - Object#=~(regexp), 如果regexp不是Regexp, 返回nil, 不抛出异常
  - a == b的意思是判断相等
    - Object#==(obj), 比较引用, 或者说比较self和obj的地址
    - String#==(str), 如果str是String, 那么比较字符串内容, 字符串必须encoding相同且bytes相同
    - Numeric#==(n), 如果n是数字, 那么转换成相同类型比较
    - Array, Hash等容器(Queue例外) #==(a), 如果a是相同类型, 那么用==比较每一个元素
  - case a; when b, 相当于b === a, 而且从上到下匹配, 只匹配一个
  - 下面的实验内容证明了以上几点

        $ ruby -v
        # => ruby 2.3.1p112 (2016-04-26 revision 54768) \[x86_64-linux\]

        1 === Integer
        # => false, #===不可交换, 由于===这个函数的self是===前面的对象

        Integer === 1
        # => true

        \[1\] === 1
        # => false, Array类没有重载#===

        (0..2) === 1
        # => true

        /abc/ === 'abc'
        # => true

        'abc' === /abc/
        # => false

        'abc' === 'abc'
        # => true, Object#===也同时包含了a==b的情况

        /123/ === /123/
        # => false, 由于Regexp类重载了#===所以上一条在这里不适用

        (1..2) === (1..2)
        # => false, 同上

        /abc/ =~ 'abc'
        # => 0, 返回匹配的位置

        'abc' =~ /abc/
        # => 0, =~看似可"交换", 这只是Object#=~和Regexp#=~行为类似而已

        1 =~ /1/
        # => nil

        /1/ =~ 1
        # TypeError
        # no implicit conversion of Fixnum into String
        # 这里可以看到, 其实=~交换操作数之后行为发生了变化

        1 == 1
        # => true

        a = Object.new; a == a.dup
        # => false

        a = 'abc'; a == a.dup
        # => true

        a = '123'.encode('utf-16')
        b = '123'.encode('utf-16').force_encoding('utf-8')
        \[a.bytes == b.bytes, a == b\]
        # => \[true, false\]


        a = \[1, 'a'\]; Marshal.restore(Marshal.dump(a)) == a
        # => true

        a = {a: 'b'}; Marshal.restore(Marshal.dump(a)) == a
        # => true


        case 1
          when 1; 1
          when Integer; Integer
          else 'else'
        end
        # => 1

        case 1
          when Integer; Integer
          when 1; 1
          else 'else'
        end
        # => Integer

        case Integer
          when 1; 1
          when Integer; Integer
          else; 'else'
        end
        # => else



- `Array` Class
  - `new`, 创建指定个数元素的数组
    - `Array.new(4) { |x| i*i }  # => [1, 4, 9, 16]`
  - `[]`, 元素和子数组

        arr = [1, 2, 3, 4, 5, 6]
        arr[2]    #=> 3
        arr[100]  #=> nil
        arr[-3]   #=> 4
        arr[2, 3] #=> [3, 4, 5]
        arr[1..4] #=> [2, 3, 4, 5]
        arr[1..-3] #=> [2, 3, 4]

  - `uniq`, 去重
  - `select`, `reject`, 过滤

        arr.select { |a| a > 3 }     #=> [4, 5, 6]
        arr.reject { |a| a < 3 }     #=> [3, 4, 5, 6]

  - `<<`, `push`, `insert`: <<是push的别名

        arr.insert(3, 'apple')  #=> [0, 1, 2, 'apple', 3, 4, 5, 6]
        arr.push('fuck')
        arr << 'fuck'

  - `collect`, `map`
  - `inject`, `reduce`
  - `size`, `length`, `count`
    - `size`, `length`: 获取数组元素个数
    - `count`: 数出满足条件的元素个数, 如果没有参数等价于`size`
  - `shuffle`, `sample`, 随机
    - `shuffle`, 打乱顺序
    - `sample(n)`, 抽出n个元素, 返回元素最多等于数组元素个数
  - `sort`, `sort_by`排序
    - `sort { |x,y| x <=> y }`: 传入的block是比较器
    - `sort_by { |x| x.size }`: 传入的是映射函数f, 将数组元素按照函数f映射后的值排序.
  - `|`, `&`, '+', '-': 逻辑运算

- `String` Class
  - `%`: 类似于printf的格式化

        "%05d" % 123                              #=> "00123"
        "%-5s: %08x" % [ "ID", self.object_id ]   #=> "ID   : 200e14d6"
        "foo = %{foo}" % { :foo => 'bar' }        #=> "foo = bar"

  - `each_char`, `each_byte`, `each_line`
  - `capitalize`, `downcase`, `upcase`
  - `center`

        "hello".center(4)         #=> "hello"
        "hello".center(20)        #=> "       hello        "
        "hello".center(20, '123') #=> "1231231hello12312312"

  - `encoding`, `force_encoding(encoding)`, `encode(encoding)`
    - `force_encoding(encoding)`: 强行把一个字符串当成另一种encoding来解析
    - `encode(encoding)`: 转换编码格式到encoding
  - `gsub(pattern, replacent)`
    - 正则表达式替换
  - `replace(str)`
    - 替换self中的字符串成为str(拷贝构造)
  - `intern`, `to_sym`: 转换为Symbol
  - `strip`

        "    hello    ".strip   #=> "hello"
        "\tgoodbye\r\n".strip   #=> "goodbye"
  - `succ`

        "abcd".succ        #=> "abce"
        "THX1138".succ     #=> "THX1139"
        "<<koala>>".succ   #=> "<<koalb>>"
        "1999zzz".succ     #=> "2000aaa"
        "ZZZ9999".succ     #=> "AAAA0000"
        "***".succ         #=> "**+"
  - `unpack(format) → anArray`
    - 将字符串中的数据转换为数组

- `Hash` Class
  - `invert`: 反转key和value
  - `key(value)`: 通过value获取key
  - `merge(hash)`: 合并, hash和self有共同的key则取hash的value

- `Kernel` Class
- `Regexp` Class
