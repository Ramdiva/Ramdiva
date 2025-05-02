// Expense submission form (React)
function ExpenseForm() {
  const [formData, setFormData] = useState({
    date: '',
    amount: '',
    category: 'travel',
    description: ''
  });

  const handleSubmit = (e) => {
    e.preventDefault();
    // API call to backend
    axios.post('/api/expenses', formData)
      .then(response => alert('Expense submitted!'));
  };

  return (
    <form onSubmit={handleSubmit}>
      {/* form fields here */}
    </form>
  );
}
