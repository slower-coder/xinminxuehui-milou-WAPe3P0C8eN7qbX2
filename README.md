
从事软件开发这么多年，平时也积累了一些方便自己快速开发的帮助类，一直在想着以什么方式分享出来，因此有了这个系列文章，后面我将以《开源\-Ideal库》系列文章分享一些我认为比较成熟、比较方便、比较好的代码，如果感觉有借鉴的地方可以集成到自己的公共代码库中，同时我也会以Nuget包的方式发布出来，以供直接下载使用。


![](https://img2024.cnblogs.com/blog/386841/202411/386841-20241106224131583-1152789529.png)


主要包括：公共、文档、ORM、SqlSugar、定时任务、Redis、Mqtt、SignalR等库封装，后面可能还会适当删减。


今天我们将分享公共库中关于时间转换的相关封装，主要是关于本地与UTC的日期、时间与时间戳和字符串之间的相互转换。


# ***01***、日期时间转时间戳（秒）


该方法是把日期时间DateTime转成10位时间戳，即秒级时间戳，代码如下：



```
/// 
/// 日期时间转时间戳（秒）
/// 
/// 日期时间
/// 时间戳（秒）
public static long ToUnixTimestampBySeconds(this DateTime dateTime)
{
    var dto = new DateTimeOffset(dateTime);
    return dto.ToUnixTimeSeconds();
}

```

# ***02***、日期时间转时间戳（毫秒）


该方法是把日期时间DateTime转为13位时间戳，即毫秒级时间戳，代码如下：



```
/// 
/// 日期时间转时间戳（毫秒）
///  
/// 日期时间
/// 时间戳（毫秒）
public static long ToUnixTimestampByMilliseconds(this DateTime dateTime)
{
    var dto = new DateTimeOffset(dateTime);
    return dto.ToUnixTimeMilliseconds();
}

```

# ***03***、时间戳（秒）转本地日期时间


该方法是把10位秒级时间戳转为本地日期时间DateTime，代码如下：



```
/// 
/// 时间戳（秒）转本地日期时间
/// 
/// 时间戳（秒）
/// 本地日期时间
public static DateTime ToLocalTimeDateTimeBySeconds(this long timestamp)
{
    var dto = DateTimeOffset.FromUnixTimeSeconds(timestamp);
    return dto.ToLocalTime().DateTime;
}

```

# ***04***、时间戳（毫秒）转本地日期时间


该方法是把13位毫秒级时间戳转为本地日期时间DateTime，代码如下：



```
/// 
/// 时间戳（毫秒）转本地日期时间
///  
/// 时间戳（毫秒）
/// 本地日期时间
public static DateTime ToLocalTimeDateTimeByMilliseconds(this long timestamp)
{
    var dto = DateTimeOffset.FromUnixTimeMilliseconds(timestamp);
    return dto.ToLocalTime().DateTime;
}

```

# ***05***、时间戳（秒）转UTC日期时间


该方法是把10位秒级时间戳转为UTC日期时间DateTime，代码如下：



```
/// 
/// 时间戳（秒）转UTC日期时间
///  
/// 时间戳（秒）
/// UTC日期时间
public static DateTime ToUniversalTimeDateTimeBySeconds(this long timestamp)
{
    var dto = DateTimeOffset.FromUnixTimeSeconds(timestamp);
    return dto.ToUniversalTime().DateTime;
}

```

# ***06***、时间戳（毫秒）转UTC日期时间


该方法是把13位毫秒级时间戳转为UTC日期时间DateTime，代码如下：



```
/// 
/// 时间戳（毫秒）转UTC日期时间
///  
/// 时间戳（毫秒）
/// UTC日期时间
public static DateTime ToUniversalTimeDateTimeByMilliseconds(this long timestamp)
{
    var dto = DateTimeOffset.FromUnixTimeMilliseconds(timestamp);
    return dto.ToUniversalTime().DateTime;
}

```

# ***07***、时间戳（秒）转本地日期


该方法是把10位秒级时间戳转为本地日期DateOnly，代码如下：



```
/// 
/// 时间戳（秒）转本地日期
///  
/// 时间戳（秒）
/// 本地日期
public static DateOnly ToLocalTimeDateBySeconds(this long timestamp)
{
    var dt = timestamp.ToLocalTimeDateTimeBySeconds();
    return DateOnly.FromDateTime(dt);
}

```

# ***08***、时间戳（毫秒）转本地日期


该方法是把13位毫秒级时间戳转为本地日期DateOnly，代码如下：



```
/// 
/// 时间戳（毫秒）转本地日期
///  
/// 时间戳（毫秒）
/// 本地日期
public static DateOnly ToLocalTimeDateByMilliseconds(this long timestamp)
{
    var dt = timestamp.ToLocalTimeDateTimeByMilliseconds();
    return DateOnly.FromDateTime(dt);
}

```

# ***09***、时间戳（秒）转UTC日期


该方法是把10位秒级时间戳转为UTC日期DateOnly，代码如下：



```
/// 
/// 时间戳（秒）转UTC日期
///  
/// 时间戳（秒）
/// UTC日期
public static DateOnly ToUniversalTimeDateBySeconds(this long timestamp)
{
    var dt = timestamp.ToUniversalTimeDateTimeBySeconds();
    return DateOnly.FromDateTime(dt);
}

```

# ***10***、时间戳（毫秒）转UTC日期


该方法是把13位毫秒级时间戳转为UTC日期DateOnly，代码如下：



```
/// 
/// 时间戳（毫秒）转UTC日期
///  
/// 时间戳（毫秒）
/// UTC日期
public static DateOnly ToUniversalTimeDateByMilliseconds(this long timestamp)
{
    var dt = timestamp.ToUniversalTimeDateTimeByMilliseconds();
    return DateOnly.FromDateTime(dt);
}

```

# ***11***、时间戳（秒）转本地时间


该方法是把10位秒级时间戳转为本地时间TimeOnly，代码如下：



```
/// 
/// 时间戳（秒）转本地时间
///  
/// 时间戳（秒）
/// 本地时间
public static TimeOnly ToLocalTimeTimeBySeconds(this long timestamp)
{
    var dt = timestamp.ToLocalTimeDateTimeBySeconds();
    return TimeOnly.FromDateTime(dt);
}

```

# ***12***、时间戳（毫秒）转本地时间


该方法是把13位毫秒级时间戳转为本地时间TimeOnly，代码如下：



```
/// 
/// 时间戳（毫秒）转本地时间
///  
/// 时间戳（毫秒）
/// 本地时间
public static TimeOnly ToLocalTimeTimeByMilliseconds(this long timestamp)
{
    var dt = timestamp.ToLocalTimeDateTimeByMilliseconds();
    return TimeOnly.FromDateTime(dt);
}

```

# ***13***、时间戳（秒）转UTC时间


该方法是把10位秒级时间戳转为UTC时间TimeOnly，代码如下：



```
/// 
/// 时间戳（秒）转UTC时间
///  
/// 时间戳（秒）
/// UTC时间
public static TimeOnly ToUniversalTimeTimeBySeconds(this long timestamp)
{
    var dt = timestamp.ToUniversalTimeDateTimeBySeconds();
    return TimeOnly.FromDateTime(dt);
}

```

# ***14***、时间戳（毫秒）转UTC时间


该方法是把13位毫秒级时间戳转为UTC时间TimeOnly，代码如下：



```
/// 
/// 时间戳（毫秒）转UTC时间
///  
/// 时间戳（毫秒）
/// UTC时间
public static TimeOnly ToUniversalTimeTimeByMilliseconds(this long timestamp)
{
    var dt = timestamp.ToUniversalTimeDateTimeByMilliseconds();
    return TimeOnly.FromDateTime(dt);
}

```

# ***15***、字符串转日期时间，转换失败则返回空


该方法是把字符串转为日期时间DateTime，转换失败则返回空，具体代码如下：



```
/// 
/// 字符串转日期时间，转换失败则返回空
/// 
/// 需转换的字符串
/// 日期时间
public static DateTime? ToDateTime(this string source)
{
    if (DateTime.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return default;
}

```

# ***16***、字符串转日期时间，转换失败则返回默认日期时间


该方法是把字符串转为日期时间DateTime，转换失败则返回默认日期时间，具体代码如下：



```
/// 
/// 字符串转日期时间，转换失败则返回默认值
/// 
/// 需转换的字符串
/// 默认日期时间
/// 日期时间
public static DateTime ToDateTimeOrDefault(this string source, DateTime dateTime)
{
    if (DateTime.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return dateTime;
}

```

# ***17***、字符串转日期，转换失败则返回空


该方法是把字符串转为日期DateOnly，转换失败则返回空，具体代码如下：



```
/// 
/// 字符串转日期，转换失败则返回空
/// 
/// 需转换的字符串
/// 日期
public static DateOnly? ToDateOnly(this string source)
{
    if (DateOnly.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return default;
}

```

# ***18***、字符串转日期，转换失败则返回默认日期


该方法是把字符串转为日期DateOnly，转换失败则返回默日期，具体代码如下：



```
/// 
/// 字符串转日期，转换失败则返回默认日期
/// 
/// 需转换的字符串
/// 默认日期
/// 日期
public static DateOnly ToDateOnlyOrDefault(this string source, DateOnly dateOnly)
{
    if (DateOnly.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return dateOnly;
}

```

# ***19***、字符串转时间，转换失败则返回空


该方法是把字符串转为日期TimeOnly，转换失败则返回空，具体代码如下：



```
/// 
/// 字符串转时间，转换失败则返回空
/// 
/// 需转换的字符串
/// 时间
public static TimeOnly? ToTimeOnly(this string source)
{
    if (TimeOnly.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return default;
}

```

# ***20***、字符串转时间，转换失败则返回默认时间


该方法是把字符串转为日期TimeOnly，转换失败则返回默认时间，具体代码如下：



```
/// 
/// 字符串转时间，转换失败则返回默认时间
/// 
/// 需转换的字符串
/// 默认时间
/// 时间
public static TimeOnly ToTimeOnlyOrDefault(this string source, TimeOnly timeOnly)
{
    if (TimeOnly.TryParse(source, CultureInfo.InvariantCulture, DateTimeStyles.None, out var date))
    {
        return date;
    }
    return timeOnly;
}

```

稍晚些时候我会把库上传至Nuget上，大家可以搜索Ideal.Core.Common直接使用。


***注***：测试方法代码以及示例源码都已经上传至代码库，有兴趣的可以看看。[https://gitee.com/hugogoos/Ideal](https://github.com)


 本博客参考[豆荚加速器](https://yirou.org)。转载请注明出处！
