Render lists of items and give flexibility for different renders based on the data

```JSX
import "./App.css";

const tahoe_peaks = [
  { name: "Freel", elevation: 10891 },
  { name: "Monument", elevation: 10067 },
  { name: "Pyramid", elevation: 9983 },
  { name: "Tallac", elevation: 9735 },
];

function List({ data, renderItem, renderEmpty }) {
  //If data.length is zero renderEmpty, else render items
  return !data.length ? (
    renderEmpty
  ) : (
    <ul>
      {data.map((item) => (
        <li key={item.name}>{renderItem(item)}</li>
      ))}
    </ul>
  );
}

//Shorhand version of React.fragment is <></>
function App() {
  return (
    <div>
      <List data={tahoe_peaks} renderEmpty={ <p>This list is empty</p> } renderItem={ (item) => <>{item.name} - {item.elevation} ft.</> } />
    </div>
  );
}

export default App;

```