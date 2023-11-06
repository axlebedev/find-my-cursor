# Vim plugin: Find my cursor
Highlight/unhighlight cursor position by any criteria.

<!-- ![image](https://user-images.githubusercontent.com/3949614/158979422-eaf84035-9222-4bf6-8a10-e0c42a120e02.png) -->

This plugin adds a function: highlight cursor position  
Highlight will be cleared after timeout, or "CursorMoved" event

``` Vim Script
:FindCursor <hexColor> <timeoutMs>
:call findcursor#FindCursor(<hexColor>, <timeoutMs>)  
```

`<hexColor>` [required] -
color in [hex format](https://www.w3schools.com/colors/colors_hexadecimal.asp), or `0` - use `CursorLine` and `CursorColumn` highlights

`<timeoutMs>` [optional, default = 0] - 
after this timeout highlight will be hidden.  
`0` - wait for "CursorMoved".  


### USAGE
Several examples

0. Run "FindCursor" from command line
``` Vim Script
:FindCursor #CC0000 500
```

1. Map "FindCursor"
``` Vim Script
nnoremap <leader>f <CMD>FindCursor #CC0000 500<CR>
noremap % %<CMD>FindCursor 0 500<CR>
```

2. Run "FindCursor" with other action (complex example)
``` Vim Script
" Using with 'neoclide/coc.nvim':
" 'jumpDefinition' runs asynchronously, so run 'FindCursor' after 100ms timeout
function! JumpDefinitionFindCursor() abort
    call CocAction("jumpDefinition")
    call timer_start(100, {id -> findcursor#FindCursor('#D6D8FA', 0)})
endfunction
nnoremap <silent> gd <CMD>call JumpDefinitionFindCursor()<CR>
```

3. Run "FindCursor" with other action (complex example 2)
``` Vim Script
" Using with plugins 'junegunn/vim-slash' and 'henrik/vim-indexed-search'
noremap <silent> <plug>(slash-after) <CMD>execute("FindCursor #d6d8fa 0<bar>ShowSearchIndex")<CR>
```


### DEMO

https://user-images.githubusercontent.com/3949614/158979017-19f3cf61-6b3e-4a23-a3b1-2b4a413e9cb4.mp4



### CONFIGURATION
##### `g:FindCursorPre`
A function to run before "FindCursor". Use for disable some other highlights if there are conflicts.
``` Vim Script
function! FindCursorHookPre() abort
    FootprintsDisable " 'axlebedev/footprints' plugin
    IlluminationDisable " 'RRethy/vim-illuminate' plugin
endfunction
let g:FindCursorPre = function('FindCursorHookPre')
```

##### `g:FindCursorPost`
Opposite to `g:FindCursorPre`: a function to run after "FindCursor" is cleared.
``` Vim Script
" Lambda function is OK too
let g:FindCursorPost = {-> execute('FootprintsEnable | IlluminationEnable')}
```

---


### NOTES
If you find a bug, or have an improvement suggestion -
please place an issue in this repository.

---


Check out my Vim plugins:   
https://github.com/axlebedev  
