// DOM Elements
const membersInput = document.getElementById('members');
const numberOfGroupsInput = document.getElementById('numberOfGroups');
const assignButton = document.getElementById('assignButton');
const resetButton = document.getElementById('resetButton');
const errorElement = document.getElementById('error');
const resultsElement = document.getElementById('results');
const groupsContainer = document.getElementById('groupsContainer');

// Event Listeners
assignButton.addEventListener('click', assignGroups);
resetButton.addEventListener('click', resetForm);

// Functions
function assignGroups() {
    hideError();
    
    // Split member names by line breaks, commas, or Japanese commas and filter out empty entries
    const memberList = membersInput.value
        .split(/[\n,、]/)
        .map(member => member.trim())
        .filter(member => member.length > 0);
    
    // Validation
    if (memberList.length === 0) {
        showError('メンバーを入力してください');
        return;
    }
    
    const groupCount = parseInt(numberOfGroupsInput.value, 10);
    
    if (isNaN(groupCount) || groupCount <= 0) {
        showError('1以上のグループ数を入力してください');
        return;
    }
    
    if (groupCount > memberList.length) {
        showError('グループ数はメンバー数以下にしてください');
        return;
    }
    
    // Shuffle the member list using Fisher-Yates algorithm
    const shuffledMembers = [...memberList];
    for (let i = shuffledMembers.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [shuffledMembers[i], shuffledMembers[j]] = [shuffledMembers[j], shuffledMembers[i]];
    }
    
    // Distribute members among groups
    const groups = Array.from({ length: groupCount }, () => []);
    
    shuffledMembers.forEach((member, index) => {
        const groupIndex = index % groupCount;
        groups[groupIndex].push(member);
    });
    
    displayGroups(groups);
}

function displayGroups(groups) {
    // Clear previous results
    groupsContainer.innerHTML = '';
    
    // Create and add group elements
    groups.forEach((groupMembers, index) => {
        const groupDiv = document.createElement('div');
        groupDiv.className = 'p-3 border rounded bg-gray-50';
        
        const groupTitle = document.createElement('h3');
        groupTitle.className = 'font-bold mb-1';
        groupTitle.textContent = `グループ ${index + 1}`;
        
        const membersList = document.createElement('ul');
        membersList.className = 'list-disc pl-5';
        
        groupMembers.forEach(member => {
            const memberItem = document.createElement('li');
            memberItem.textContent = member;
            membersList.appendChild(memberItem);
        });
        
        groupDiv.appendChild(groupTitle);
        groupDiv.appendChild(membersList);
        groupsContainer.appendChild(groupDiv);
    });
    
    // Show results section
    resultsElement.classList.remove('hidden');
}

function showError(message) {
    errorElement.textContent = message;
    errorElement.classList.remove('hidden');
}

function hideError() {
    errorElement.textContent = '';
    errorElement.classList.add('hidden');
}

function resetForm() {
    membersInput.value = '';
    numberOfGroupsInput.value = '2';
    hideError();
    resultsElement.classList.add('hidden');
    groupsContainer.innerHTML = '';
}
