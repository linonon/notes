1. 對於 struct, 按需開關字段, 但是修改字段需要使用 setter 方法, 保證代碼的可閱讀性.
```go
type Worker interface {
	DoJob()
}

type Person struct {
	Name string
	Age int
}

type FBI struct {
	Person

	Energy int
}

func NewFBI(name string, age int) *FBI {
	return &FBI{
		Name: name,
		Age: age,
	}
}

func (f *FBI) DoJob() {
	fmt.Printf("%s is %d years old, now do job")
	err := f.DecreaseEnergy(10)
	if err != nil {
		fmt.Println()
	}
}

func (f *FBI) SetEnergy(e int) error {
	if e <= 0 {
		return  fmt.Errorf("energy empty")
	}
	f.Energy = e
}

func (f *FBI) DecreaseEnergy(e int) error {
	f.Energy -= e
}

func main() {
	fbi := NewFBI("gorge", 25)
	fbi.SetEnergy(100)
	fmt.Printf("now %s has %d energy", fbi.Name, fbi.Energy)
}
```