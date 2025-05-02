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
// ExpenseForm.test.js
import { render, screen, fireEvent } from '@testing-library/react';
import ExpenseForm from './ExpenseForm';

test('submits expense data correctly', () => {
  const mockSubmit = jest.fn();
  render(<ExpenseForm onSubmit={mockSubmit} />);
  
  fireEvent.change(screen.getByLabelText('Amount'), { target: { value: '50' } });
  fireEvent.click(screen.getByText('Submit'));
  
  expect(mockSubmit).toHaveBeenCalledWith({ amount: '50' });
});
// expenses-api.test.js
const request = require('supertest');
const app = require('../server');

describe('Expenses API', () => {
  it('POST /api/expenses creates a new expense', async () => {
    const res = await request(app)
      .post('/api/expenses')
      .send({ amount: 100, category: 'meals' });
    
    expect(res.status).toBe(201);
    expect(res.body).toHaveProperty('id');
  });
// expenses-api.test.js
const request = require('supertest');
const app = require('../server');

describe('Expenses API', () => {
  it('POST /api/expenses creates a new expense', async () => {
    const res = await request(app)
      .post('/api/expenses')
      .send({ amount: 100, category: 'meals' });
    
    expect(res.status).toBe(201);
    expect(res.body).toHaveProperty('id');
  });
// expense-submission.spec.js
describe('Expense Submission', () => {
  it('lets a user submit an expense', () => {
    cy.loginAsEmployee();
    cy.visit('/expenses/new');
    cy.get('#amount').type('75');
    cy.get('form').submit();
    cy.contains('Expense submitted successfully');
  });
project-root/
├── src/
│   ├── components/
│   │   ├── ExpenseForm.js
│   │   └── ExpenseForm.test.js  # Unit tests
│   ├── api/
│   │   ├── expenses.js
│   │   └── expenses.test.js     # API tests
├── cypress/
│   ├── e2e/
│   │   └── expense-flows.spec.js # E2E tests
└── jest.config.js
