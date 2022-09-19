# PC Keyboard on MacOS

If you have a PC-style keyboard with separate `home`, `end`, `page up` and `page down` keys, you've likely noticed they don't always work like you would expect on macOS, especially if you are used to the behavior in Windows. 

Thanks to [this blog](https://damieng.com/blog/2015/04/24/make-home-end-keys-behave-like-windows-on-mac-os-x/), it's easy to configure macOS to behave like that. 

In a terminal run the following, which will run [this script](https://gist.github.com/Levent0z/731f0c4810310bc3e2674882f88b7c23):

```bash
/bin/bash -c "$(curl -fsSL https://gist.githubusercontent.com/Levent0z/731f0c4810310bc3e2674882f88b7c23/raw/f60c3b0df53def7fcb81496e473ea94ae53a6d68/genKeyBindings.sh)"
```
