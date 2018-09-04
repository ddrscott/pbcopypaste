# A Tale of Two Besties: `pbcopy` and `pbpaste`

## OS X High School

`pbcopy` and `pbpaste` were the new kids at OSX High School. All the students picked on them because they could never do anything on their own. Teachers thought they were weird for always playing with pipes.

## Blank Page

On the first day after winter break, the school website was rendering blank pages. No one could see their calendars or agendas and the IT guy was stuck in Bermuda.

## Ada

Ada, the STEM lab assistant, thought she'd better take a look. She started by poking around in the browser's devtools. The responses were all 200s, but there were some console errors:


## Eureka!
```
Can't read property 'event_dt' of undefined.
```

"Eureka!", Ada exclaimed. "The JSON response must have changed!"

## Too Much Text

She quickly went to the response tab and tried to preview the data, but there was too much for her browser to handle. She copied the response using CMD-a and CMD-c, and tried to paste it into her editor. Alas, the editor kept freezing trying to format the huge amount of text!

## pbpaste

`pbpaste` wandered by noticing the frustration in Ada's slouch.

She came right up to Ada and said, "Um, I can put that JSON in a file for you. Would you mind if I took a shot at it?"

"Go ahead", scoffed Ada in disbelief, "Let's see what you can do."

## Paste to File

```sh
pbpaste > data.json
```

Ada was shocked. "Wha, WHAT?! How'd you do that so fast?!" she exclaimed.

`pbpaste` responded, "It's because I have direct access to the pasteboard. I can read it to any file or command. Watch this! I can pipe my output to `jq` to pretty format the JSON. All without a bloated IDE slowing things down."

```sh
pbpaste | jq . > formatted.json
```

## pbcopy

"I can also work with my bestie, `pbcopy`, to get the results back into the pasteboard!"

`pbpaste` yelled down the hallway, "`pbcopy` get over here! Let's show Ada our sweet moves!"

```
pbpaste | jq . | pbcopy
```

`pbcopy` sat back as if she'd just finished a big meal. She pushed up her glasses and added, "When I work together with `pbpaste`, you won't need to waste brain cells thinking of clever temporary file names!"

## Rails Console

Ada wanted to bring them down a notch. She stated, "This is great when I'm in shell, but I usually have all my data in Rails objects from within the console. Then what?"

Leaning forward, `pbcopy` responded, "That's even better! When you're in IRB, try piping the data straight to me."

## `popen`
```ruby
IO.popen('jq . | `pbcopy`', 'w'){|io| io << items.to_json}
```

## One Liner
```ruby
IO.popen('jq . | `pbcopy`', 'w'){|❤️| ❤️ << items.to_json}
```

"Furthermore", `pbcopy` says, "if you want to read from the clipboard, use backticks!"

```ruby
lines = `pbpaste`.split("\n")
```

## But Wait There's More

Together, they were so excited and said at the same time, "We have this snippet in our `~/.pryrc` which makes working with us even easier!"

```ruby
def copy(data=nil)
  IO.popen('pbcopy', 'w') do |io| 
    if block_given?
      yield io
      puts "\e[34mCopied block!\e[0m"
    elsif data
      io << data.to_s
      puts "\e[34mCopied data!\e[0m"
    else
      puts "\e[31mNothing to copy :(\e[0m"
      puts "\e[34m  Try `copy { |c| c << data }`"
      puts "   or `copy data`\e[0m"
    end
  end
end
```

They continued, "Now, in Pry we can use `copy _` to send the last result to the pasteboard!"

## Typo

In the midst of all the terminal output and pretty formatted JSON, `pbpaste` noticed an odd misspelling.

```json
{
  posts: ["..."]
  aggendas: ["..."]
}
```

## Solved

"This is what must be causing the undefined error! Isn't ajjenda spelled with 'j's?" `pbpaste` asked.

`pbcopy` jumped in quickly, "Correction, it only has _one_ 'j'!"

Ada, finally smiling, replied "You two were made for each other!"

## The End

###### Production Tools

- Vim
- Reveal.js
- http://paletton.com/#uid=75i0u0k5uTk00++29Z49uK7e4y1
- https://www.canva.com/color-palette/
- http://www.colorzilla.com/gradient-editor/
- https://fonts.google.com/
