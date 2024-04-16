```
import { useEffect, useState } from "react";

function useDebounce(value, delay = 300) { 
  const [debouncedValue, setDebouncedValue] = useState(value); 
  useEffect(() => {
    const handler = setTimeout(() => { setDebouncedValue(value); }, delay);
    return () => { 
      clearTimeout(handler); 
    };
  }, [value, delay]);
  return debouncedValue;
}

function App() {
  const [value, setValue] = useState("");
  const debouncedValue = useDebounce(value, 300);

  useEffect(() => {
    if (debouncedValue) {
      fetch(`http//localhost/api/query=${debouncedValue}`)
    }
  }, [debouncedValue]);

  return (
    <div className="p-4 container mx-auto">
      <h3 className="text-2xl font-bold">Debounce</h3>
      <input
        className="w-full p-2 border border-gray-300 rounded mt-2"
        placeholder="Search..."
        onChange={(e) => setValue(e.target.value)}
        type="text"
      />
      <p>
        Yazılan Değer = <span className="font-bold"> {value}</span>
      </p>
      <p>
        Yazılan Değer Debounce = <span className="font-bold"> {debouncedValue}</span>
      </p>
    </div>
  );
}

export default App;