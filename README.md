# Renton Technical College CSI-246

<div align="center">  
    <img src="logo.jpg" alt="Logo">
    <h3 align="center">Independent Activity 2</h3>
</div>

## Overview

In this independent activity, you will create a vehicle sales website using Next.js 15. You'll apply the concepts learned in Guided Activity 2, including:
- Server and Client Components
- Dynamic Routes
- Data Handling
- Error and Loading States

## Requirements

Create a vehicle sales website with the following features:

1. **Vehicle List Page** (`/vehicles`)
   - Display a grid or list of available vehicles
   - Each vehicle card should show:
     * Vehicle image (you can use placeholder images)
     * Year, make, and model
     * Price
     * Brief description
     * Link to details page

2. **Vehicle Details Page** (`/vehicles/[id]`)
   - Show complete vehicle information
   - Display all vehicle specifications
   - Form for users to leave comments
   - Page updates when a comment is added
   - You don't need to worry about saving the comments to persistent storage for now

3. **Required Technical Features**
   - Use Server Components for data fetching
   - Implement loading.tsx for both pages
   - Add error.tsx for error handling
   - Use proper TypeScript types
   - Create utility functions as needed
   - Follow the project structure from Guided Activity 2

## Sample Data - Here is some sample data to get you started.

Copy this data into `app/lib/data.ts`:

```typescript
export type Vehicle = {
  id: string;
  year: number;
  make: string;
  model: string;
  price: number;
  description: string;
  specs: {
    engine: string;
    transmission: string;
    mileage: number;
    exteriorColor: string;
    interiorColor: string;
    fuelType: string;
  };
  features: string[];
  image: string;
  comments: Comment[];
};

export type Comment = {
  id: string;
  author: string;
  text: string;
  date: Date;
};

const vehicles: Vehicle[] = [
  {
    id: "1",
    year: 2023,
    make: "Toyota",
    model: "Camry",
    price: 27999,
    description: "Sleek and reliable sedan with excellent fuel economy",
    specs: {
      engine: "2.5L 4-Cylinder",
      transmission: "8-Speed Automatic",
      mileage: 15000,
      exteriorColor: "Midnight Black",
      interiorColor: "Beige",
      fuelType: "Gasoline"
    },
    features: [
      "Adaptive Cruise Control",
      "Lane Departure Warning",
      "Apple CarPlay Integration",
      "Blind Spot Monitor",
      "LED Headlights"
    ],
    image: "https://placehold.co/600x400/234/fff",
    comments: [
      {
        id: "c1",
        author: "John Smith",
        text: "Great family car, very comfortable ride!",
        date: new Date("2024-01-05")
      }
    ]
  },
  {
    id: "2",
    year: 2024,
    make: "Honda",
    model: "CR-V",
    price: 32999,
    description: "Versatile SUV perfect for family adventures",
    specs: {
      engine: "1.5L Turbo 4-Cylinder",
      transmission: "CVT",
      mileage: 5000,
      exteriorColor: "Platinum White",
      interiorColor: "Gray",
      fuelType: "Gasoline"
    },
    features: [
      "Honda Sensing Suite",
      "Wireless Phone Charging",
      "Panoramic Sunroof",
      "Power Tailgate",
      "AWD System"
    ],
    image: "https://placehold.co/600x400/808/fff",
    comments: [
      {
        id: "c2",
        author: "Sarah Johnson",
        text: "Love the safety features and spacious interior!",
        date: new Date("2024-01-08")
      }
    ]
  }
];

export async function getVehicles(): Promise<Vehicle[]> {
  // Simulate API delay
  await new Promise(resolve => setTimeout(resolve, 1000));
  return vehicles;
}

export async function getVehicle(id: string): Promise<Vehicle | null> {
  const allVehicles = await getVehicles();
  return allVehicles.find(vehicle => vehicle.id === id) || null;
}

export async function addComment(
  vehicleId: string, 
  comment: Omit<Comment, 'id' | 'date'>
): Promise<Comment> {
  // In a real app, this would be an API call
  const newComment: Comment = {
    id: Math.random().toString(36).substr(2, 9),
    ...comment,
    date: new Date()
  };
  
  // Find the vehicle and add the comment
  const vehicle = vehicles.find(v => v.id === vehicleId);
  if (!vehicle) {
    throw new Error('Vehicle not found');
  }
  
  vehicle.comments.push(newComment);
  return newComment;
}
```

## Implementation Guidelines

1. **Project Setup**
   - Create a new Next.js project following Guided Activity 2 setup steps
   - Copy the sample data into your project
   - Plan your component structure

2. **Vehicle List Page**
   - Fetch and display all vehicles
   - Design an attractive card layout
   - Implement loading and error states
   - Use Server Components for data fetching

3. **Vehicle Details Page**
   - Create a dynamic route using [id]
   - Show all vehicle information in a clean layout
   - Implement the comment system
   - Handle loading and error states

4. **Comment System**
   - Create a Component for the comment form
   - Allow users to submit new comments
   - Display all comments with dates

## Submission

1. Ensure all features are working
2. Commit your changes:
```bash
git add .
git commit -m "Independent Activity 2 Complete"
git push
```

3. Verify your repository contains:
   - All required pages and components
   - Proper loading and error states
   - Comment functionality
   - Complete TypeScript types
   - Working data fetching

If you have any questions about this assignment, please reach out to your instructor or TA for this course.
