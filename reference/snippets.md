# Snippets

> [返回参考](/reference/)

## VSCode Snippets

### Go snippets

Prefix | Description             | Prefix   | Description
-------|-------------------------|----------|----------------------------------------
im     | import                  | fp       | fmt.Println()
ims    | import block            | ff       | fmt.Printf()
co     | a constant              | lp       | log.Println()
cos    | a constant block        | lf       | log.Printf()
tyi    | a type interface        | lv       | log.Printf() with variable content
tys    | a struct declaration    | tl       | t.Log()
pkgm   | main package & function | tlf      | t.Logf()
func   | function declaration    | tlv      | t.Logf() with variable content
var    | a variable              | wr       | $1 http.ResponseWriter, $2 http.Request
switch | switch statement        | hf       | http.HandleFunc()
sel    | select statement        | hand     | http handler declaration
cs     | case clause             | rd       | http.Redirect()
for    | a for loop              | herr     | http.Error()
forr   | a for range loop        | las      | http.ListenAndServe
ch     | a channel               | sv       | http.Serve
map    | a map                   | go       | anonymous goroutine declaration
in     | empty interface         | gf       | goroutine declaration
if     | if statement            | df       | defer statement
el     | else branch             | tf       | Test function
ie     | if else                 | bf       | Benchmark function
iferr  | if err != nil {...}     | ef       | Example function
make   | make statement          | tdt      | table driven test
new    | new statement           | finit    | init function
pn     | panic                   | fmain    | main function
       |                         | meth     | method declaration
       |                         | helloweb | sample hello world webapp
       |                         | sort     | sort interface implementation