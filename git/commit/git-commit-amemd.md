# git-commit-amemd 修改提交信息



### 修改提交日期


```bash

# git commit --amend --date="commit_time"
git commit --amend --date="Fir, 05 Aug 2022 23:59:59 +0800"

```



commit 有三种格式


>  https://git-scm.com/docs/git-commit#_date_formats
> DATE FORMATS
> The `GIT_AUTHOR_DATE` and `GIT_COMMITTER_DATE` environment variables support the following date formats:
> Git internal format
> It is `<unix-timestamp> <time-zone-offset>`, where `<unix-timestamp>` is the number of seconds since the UNIX epoch. `<time-zone-offset>` is a positive or negative offset from UTC. For example CET (which is 1 hour ahead of UTC) is `+0100`.
> RFC 2822
> The standard email format as described by RFC 2822, for example `Thu, 07 Apr 2005 22:13:13 +0200`.
> ISO 8601
> Time and date specified by the ISO 8601 standard, for example `2005-04-07T22:13:13`. The parser accepts a space instead of the `T` character as well. Fractional parts of a second will be ignored, for example `2005-04-07T22:13:13.019` will be treated as `2005-04-07T22:13:13`.
>Note
>In addition, the date part is accepted in the following formats: `YYYY.MM.DD`, `MM/DD/YYYY` and `DD.MM.YYYY`.
>In addition to recognizing all date formats above, the `--date` option will also try to make sense of other, more human-centric date formats, such as relative dates like "yesterday" or "last Friday at noon".

也就是：
- RFC 2822 ==> Sun, 07 Aug 2022 23:59:59 +0800
- ISO 8601 ==> 2022-0805T23:59:59
- Note  ==>   `YYYY.MM.DD`, `MM/DD/YYYY` and `DD.MM.YYYY`...





RFC 2822 的日期与时间输出格式可以用Linux命令 :

```bash

$ date -R
Sun, 07 Aug 2022 23:59:59 +0800

```

如果我用过RFC 2922 的格式提交代码

```bash

$ git commit --amend --date="$ (date -R) "

or

$ git commit --amend --date="date -R"


```


----------

参考：

1. https://git-scm.com/docs/git-commit#_date_formats
2. [[linux-date]]
3. [git 修改上次git commit的时间](https://blog.csdn.net/guoyajie1990/article/details/73824732?spm=1001.2101.3001.6661.1&utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-73824732-blog-115652054.pc_relevant_multi_platform_featuressortv2dupreplace&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7ECTRLIST%7Edefault-1-73824732-blog-115652054.pc_relevant_multi_platform_featuressortv2dupreplace&utm_relevant_index=1)
4. [详解git commit --date的参数格式](https://juejin.cn/post/6867769352721498125)