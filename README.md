clc
clear

% Standard form matrices
A = [1  1  1  1  0  0;
     2 -1  0  0  1  0;
     1  1  0  0  0  1];

b = [4; 7; 1];
c = [2 1 1 0 0 0];

m = size(A,1);
n = size(A,2);

pairs = nchoosek(1:n, m);
nCm = size(pairs,1);

sol = [];
Z = [];

for i = 1:nCm
    x = zeros(n,1);
    A1 = A(:, pairs(i,:));
    
    if rank(A1) == m
        x(pairs(i,:)) = A1\b;
        
        if all(x >= 0)
            sol = [sol x];
            Z = [Z c*x];
        end
    end
end

% Display all BFS
result = array2table([sol' Z'], 'VariableNames',{'x1','x2','x3','s1','s2','s3','Z'})

% Find optimal solution
[maxZ, idx] = max(Z);

% Display optimal solution
optimal = array2table([sol(:,idx)' maxZ], 'VariableNames',{'x1','x2','x3','s1','s2','s3','Z'})
