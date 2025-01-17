Sure, here's the schema and resolver code:

```graphql
# schema-codegen-start
const typeDefs = `
  type Credit_Union {
    id: ID!
    Contract_Number: String!
    Credit_Union_Name: String!
    premium_reports: [Premium_Report!]!
    premium_adjustments: [Premium_Adjustment!]!
    single_premium_certificate_returns: [Single_Premium_Certificate_Return!]!
  }

  type Premium_Report {
    id: ID!
  }

  type Premium_Adjustment {
    id: ID!
    Product_Name: String!
    Report_Period: String!
    Status: String!
    Last_Update: String!
    Period_Ending: String!
    Adjustment_Type_to_the_Credit_Union: String!
    Comment: String!
    Total_Borrower_Fees_: Float!
    CU_Retail_Rate: Float!
    Protected_Loan_Amount: Float!
    Pay_Rate: Float!
    Premium_Due: Float!
    Total_Amount: Float!
  }

  type Single_Premium_Certificate_Return {
    id: ID!
  }

  input CreditUnionInput {
    id: ID
    Contract_Number: String
    Credit_Union_Name: String
  }

  type Query {
    searchCreditUnionByContractNumber(contractNumber: String!): [Credit_Union!]!
    searchCreditUnionByName(name: String!): [Credit_Union!]!
    searchCreditUnionByState(state: String!): [Credit_Union!]!
    searchCreditUnionByNameAndState(name: String!, state: String!): [Credit_Union!]!
  }

  type Mutation {
    addCreditUnion(input: CreditUnionInput!): Credit_Union!
    updateCreditUnion(id: ID!, input: CreditUnionInput!): Credit_Union!
    deleteCreditUnion(id: ID!): Boolean!
  }
`;
# schema-codegen-end
```

```javascript
// resolver-codegen-start
const sampleCreditUnions = [
  {
    id: '1',
    Contract_Number: '12345',
    Credit_Union_Name: 'ABC Credit Union',
    premium_reports: [],
    premium_adjustments: [],
    single_premium_certificate_returns: []
  },
  // Add more sample data here
];

const resolvers = {
  Query: {
    searchCreditUnionByContractNumber: (parent, args) => {
      return sampleCreditUnions.filter(
        (cu) => cu.Contract_Number === args.contractNumber
      );
    },
    searchCreditUnionByName: (parent, args) => {
      return sampleCreditUnions.filter(
        (cu) => cu.Credit_Union_Name.includes(args.name)
      );
    },
    searchCreditUnionByState: (parent, args) => {
      // Implement filtering logic based on state
      return [];
    },
    searchCreditUnionByNameAndState: (parent, args) => {
      // Implement filtering logic based on name and state
      return [];
    },
  },
  Mutation: {
    addCreditUnion: (parent, args) => {
      const newCreditUnion = { id: Date.now().toString(), ...args.input };
      sampleCreditUnions.push(newCreditUnion);
      return newCreditUnion;
    },
    updateCreditUnion: (parent, { id, input }) => {
      const index = sampleCreditUnions.findIndex((cu) => cu.id === id);
      if (index !== -1) {
        sampleCreditUnions[index] = { ...sampleCreditUnions[index], ...input };
        return sampleCreditUnions[index];
      }
      throw new Error('Credit Union not found');
    },
    deleteCreditUnion: (parent, { id }) => {
      const index = sampleCreditUnions.findIndex((cu) => cu.id === id);
      if (index !== -1) {
        sampleCreditUnions.splice(index, 1);
        return true;
      }
      return false;
    },
  },
};
// resolver-codegen-end
```